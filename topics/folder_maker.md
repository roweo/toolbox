---
title: folder_maker
date: 2022-01-05
draft: false
keyword: 
    - Keyword 1
    - Keyword 2
---

# Folder maker script

An example that builds a hierarchy of folders including looping through a custom [text file](#input-text-file) for creating subfolders.

``` shell
@ECHO OFF
REM %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
REM     *ProjectBuilder*   
REM     Created by: Owen Rowe    
REM     Date: 2021-12-23        
REM %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

@ECHO +================= BEFORE ENTERING LABEL REQUEST NUMBER BELOW =====================+
@ECHO *                                                                                  * 
@ECHO *   This script will take a user filtered list from the 'Label Project             *
@ECHO *      Tracker' and build the appropriate folders for your project                 *
@ECHO *                                                                                  *
@ECHO *      1. Filter your project list in the 'Label Project Tracker'                  *
@ECHO *      2. Click the toolbar 'copy' button to copy to clipboard                     *
@ECHO *      3. Paste your clipboard contents into the 'pastefile.txt' and SAVE it!      *
@ECHO *      4. Enter your LR number below and hit 'enter'                               *
@ECHO *                                                                                  *
@ECHO +==================================================================================+
@ECHO.
@ECHO OFF


REM Prompt for Label request number (LRnum) here

set /p LRnum="Enter LR number: "

REM Build standard folder set using LR-%LRnum% as parent directory

md "LR-%LRnum%"
md "LR-%LRnum%\1- INPUT FORMS"
md "LR-%LRnum%\2- ARTWORKS"
md "LR-%LRnum%\3- PROOFREADING"
md "LR-%LRnum%\4- SPECIFICATIONS"
md "LR-%LRnum%\5- PACKAGE AND QUALITY CHECK"
md "LR-%LRnum%\6- EMAIL CORRESPONDENCE"

REM cd into '.\2-ARTWORKS' folder

cd "LR-%LRnum%\2- ARTWORKS"

REM This loops through the pastefile.txt with options: 'skip' first three lines, take the first item ('token') encountered, delimited ('delims') by TAB character. The tokens are then used to create the GL subfolders

FOR /f "skip=3 tokens=1 delims=	" %%G in (..\..\pastefile.txt) do mkdir %%G\Artwork %%G\Specification %%G\Comms

REM Message box to give user feedback that the process has completed

echo msgbox "Project files created!" ^& vbNewLine ^& vbNewLine ^& "Click 'OK' to close this dialog" > "%temp%\popup.vbs"
wscript.exe "%temp%\popup.vbs"
```

## Input text file

``` text
*** THIS IS SAMPLE CONTENT ONLY - Select everything (Ctrl-A) and replace with your clipboard content (Ctrl-V) :) ***

GL Number	LR Number	Title	GBU	Project Leader	Project State
GL-007074	LR-1711	Prismaflex/Oxiris (CE mark) for worldwide	Acute Therapies	Annabelle Harrison	Active
GL-007073	LR-1711	Prismaflex/Oxiris (CE mark) for worldwide	Acute Therapies	Annabelle Harrison	Active
GL-007072	LR-1711	Prismaflex/Oxiris (CE mark) for worldwide	Acute Therapies	Annabelle Harrison	Active
GL-007071	LR-1711	Prismaflex/Oxiris (CE mark) for worldwide	Acute Therapies	Annabelle Harrison	Active
GL-007070	LR-1711	Prismaflex/Oxiris (CE mark) for worldwide	Acute Therapies	Annabelle Harrison	Active
GL-007069	LR-1711	Prismaflex/Oxiris (CE mark) for worldwide	Acute Therapies	Annabelle Harrison	Active
GL-007068	LR-1711	Prismaflex/Oxiris (CE mark) for worldwide	Acute Therapies	Annabelle Harrison	Active
GL-007067	LR-1711	Prismaflex/Oxiris (CE mark) for worldwide	Acute Therapies	Annabelle Harrison	Active
GL-007066	LR-1711	Prismaflex/Oxiris (CE mark) for worldwide	Acute Therapies	Annabelle Harrison	Active
GL-007065	LR-1711	Prismaflex/Oxiris (CE mark) for worldwide	Acute Therapies	Annabelle Harrison	Active
GL-007064	LR-1711	Prismaflex/Oxiris (CE mark) for worldwide	Acute Therapies	Annabelle Harrison	Active
GL-007063	LR-1711	Prismaflex/Oxiris (CE mark) for worldwide	Acute Therapies	Annabelle Harrison	Active
GL-007062	LR-1711	Prismaflex/Oxiris (CE mark) for worldwide	Acute Therapies	Annabelle Harrison	Active
GL-006606	LR-1711	Prismaflex/Oxiris (CE mark) for worldwide	Acute Therapies	Annabelle Harrison	Active
```