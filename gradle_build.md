# Gradle build

CMD `gradle dita`

``` java
plugins {
    id 'de.undercouch.download' version '4.1.1'
	id 'com.github.eerohele.dita-ot-gradle' version '0.7.1'
}

def ditaOtVersion = '3.6.1'

// Download and install DITA-OT

task downloadDitaOt(type: Download) {
    src "https://github.com/dita-ot/dita-ot/releases/download/${ditaOtVersion}/dita-ot-${ditaOtVersion}.zip"
    dest new File(buildDir, "dita-ot-${ditaOtVersion}.zip")
    overwrite false
}

task extract(dependsOn: downloadDitaOt, type: Copy) {
    from zipTree(downloadDitaOt.dest)
    into buildDir
}

def ditaHome = "${buildDir}/dita-ot-${ditaOtVersion}"

// Install DITA-OT plugins from DITA-OT Plugin Registry

def plugins = ['org.lwdita', 'org.dita.normalize']

plugins.each { id ->
    tasks.create(id, Exec) {
        // Install plugin if not already installed, otherwise build will fail
        onlyIf { !file("$ditaHome/plugins/$id").exists() }
        outputs.dir("$ditaHome/plugins/$id")
        workingDir ditaHome
        commandLine 'bin/dita', '--install', id
    }
}

task install(dependsOn: [extract, plugins])

// Publish my.ditamap into the PDF output format.
dita {
    dependsOn install
    ditaOt ditaHome
    singleOutputDir true
    useAssociatedFilter true
    input fileTree(dir: '.', include: '*.ditamap')
    transtype 'pdf2'
}

defaultTasks 'dita'
```
