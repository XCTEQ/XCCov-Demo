#  xccov - Xcode Code Coverage for Humans 

With Xcode 9.3, we have new command line tool `xccov` to view Xcode Code Coverage Reports in human readable format. 

This is quick demo of the `xccov` command line utility with black app. 

## Pre-requisite 

* Xcode 9.3 


## Generate Code Coverage Data 

Clone this repository and build an app from command line. 

            $ git clone 
            $ cd XCCov-Demo
            $ xcodebuild -project XCCov-Demo.xcodeproj/ -scheme XCCov-Demo -derivedDataPath Build/ -destination 'platform=iOS Simulator,OS=12.2,name=iPhone Xʀ' -enableCodeCoverage YES clean build test CODE_SIGN_IDENTITY="" CODE_SIGNING_REQUIRED=NO

This will dump all the `DerivedData` inside the `Build` directory. 

This will generate the code coverage data at path `Build/Logs/Test/Run-{projectName_timestamp}.xcresult/3_Test  ` we will see code coverage with 
`.xccovreport` and `.xccovarchive` extension. The cov-
erage report contains line coverage percentages for each target, source file, and function/method that has coverage  infor-
mation.  The  coverage  archive contains the raw execution counts for each file in the report.

## Using `xccov`

We can use `xccov` command line tool with `xcrun` untility if thats not inside the `$PATH` 

* View Report in the plain format 

            $ xcrun xccov view Build/Logs/Test/Run-XCCov-Demo-2019.04.03_07-40-58-+0100.xcresult/3_Test/action.xccovreport

*  View Report in the JSON format 

            $ xcrun xccov view --json Build/Logs/Test/Run-XCCov-Demo-2019.04.03_07-40-58-+0100.xcresult/3_Test/action.xccovreport

* List the files available for the code coverage data 

            $ xcrun xccov view --file-list Build/Logs/Test/Run-XCCov-Demo-2019.04.03_07-40-58-+0100.xcresult/3_Test/action.xccovarchive

* Show the coverage for perticular file 
        
            $ xcrun xccov view --file ~/Desktop/XCCov-Demo/XCCov-Demo/AppDelegate.swift  Build/Logs/Test/Run-XCCov-Demo-2019.04.03_07-40-58-+0100.xcresult/3_Test/action.xccovarchive/


* Merge Reports 

            $ xcrun xccov merge --outReport ~/Desktop/out.xccovreport --outArchive ~/Desktop/out.acarchive Build/Logs/Test/Run-XCCov-Demo-2019.04.03_07-40-58-+0100.xcresult/3_Test/action.xccovreport Build/Logs/Test/Run-XCCov-Demo-2019.04.03_07-40-58-+0100.xcresult/3_Test/action.xccovarchive/ Build/Logs/Test/Run-XCCov-Demo-2019.04.03_07-52-58-+0100.xcresult/3_Test/action.xccovreport Build/Logs/Test/Run-XCCov-Demo-2019.04.03_07-52-58-+0100.xcresult/3_Test/action.xccovarchive/
This will create merge reports file on desktop. 
