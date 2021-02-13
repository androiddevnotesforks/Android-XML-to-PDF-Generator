<!-- ⚠️ This README has been generated from the file(s) "blueprint.md" link - https://github.com/andreasbm/readme ⚠️--><p align="center">
  <img src="https://github.com/Gkemon/Android-XML-to-PDF-Generator/blob/master/logo.png" alt="Logo" width="150" height="150"  />
</p>
<h1 align="center">XML to PDF Generator For Android</h1>
 <p align="center">
		<a href="https://github.com/Gkemon/XML-to-PDF-generator"><img alt="Maintained" src="https://img.shields.io/badge/Maintained%3F-yes-green.svg" height="20"/></a>
	<a href="https://github.com/Gkemon/XML-to-PDF-generator"><img alt="Maintained" src="https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg" height="20"/></a>
	</p>
	 <p align="center">
	<a href="https://android-arsenal.com/details/1/8165"><img alt="Maintained" src="https://img.shields.io/badge/Android%20Arsenal-Android--XML--to--PDF--Generator-green.svg?style=flat" height="20"/></a>
	</p>

</p>

<p align="center">
  <b>Automatically generate PDF file from XML file or Java's View object in Android</b></br>
  <p align="center"> Make PDF from Android layout resources (e.g - R.layout.myLayout,R.id.viewID), Java's view ids or directly views objects <p>
</p>

<br />


<p align="center">
  <!-- GIF <img src="https://raw.githubusercontent.com/andreasbm/readme/master/assets/demo.gif" alt="Demo" width="800" /> --!>
</p>

* **Simple**: Extremely simple to use. For using <b>Step Builder Design Patten</b> undernath,here IDE greatly helps developers to complete the steps for creating a PDF from XMLs.
* **Powerful**: Customize almost everything.
* **Transparent**: It shows logs,success-responses, failure-responses , that's why developer will nofity any event inside the process. 

<details>
<summary>📖 Table of Contents</summary>
<br />

[![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/colored.png)](#table-of-contents)

## ➤ Table of Contents

* [➤ Installation](#-installation)
* [➤ Getting Started](#-getting-started)
* [➤ License](#-license)
</details>


[![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/colored.png)](#installation)

## ➤ Installation

**Step 1**. Add the JitPack repository to your root ```build.gradle``` at the end of repositories
```
/
android {
 .
 .
 .
 .
  
   /*Need Java version 1.8 as Rx java is used for file write underneath for preventing UI freezing*/
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
 .
 .
 .

}
 .
 .
 .
allprojects {
    repositories {
        // ...
        maven { url 'https://jitpack.io' }
    }
}
.
.
.
```

**Step 2**. Add the dependency
```
dependencies {
        implementation 'com.github.Gkemon:XML-to-PDF-generator:1.0'
}
```	
[![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/colored.png)](#getting-started-quick)



## ➤ Getting Started

You can generate <b>PDF</b> from many sources.
* Layout resources (i.e: ```R.layout.myLayout```)
* View ids (i.e: ```R.id.viewID```)
* Java view objects (i.e ```View```,```TextView```,```LinearLayout```)



### From layout resources :


```java
 PdfGenerator.getBuilder()
                        .setContext(context)
                        .fromLayoutXMLSource()
                        .fromLayoutXML(R.layout.layout_print,R.layout.layout_print)
			/* "fromLayoutXML()" takes array of layout resources.
			 * You can also invoke "fromLayoutXMLList()" method here which takes list of layout resources instead of array. */
                        .setDefaultPageSize(PdfGenerator.PageSize.A4)
			/* It takes default page size like A4,A5,WRAP_CONTENT. You can also set custom page size in pixel
			 * by calling ".setCustomPageSize(int widthInPX, int heightInPX)" here. */
                        .setFileName("Test-PDF")
			/* It is file name */
                        .setFolderName("FolderA/FolderB/FolderC")
			/* It is folder name. If you set the folder name like this pattern (FolderA/FolderB/FolderC), then
			 * FolderA creates first.Then FolderB inside FolderB and also FolderC inside the FolderB and finally
			 * the pdf file named "Test-PDF.pdf" will be store inside the FolderB. */
                        .openPDFafterGeneration(true)
			/* It true then the generated pdf will be shown after generated. */
                        .build(new PdfGeneratorListener() {
                            @Override
                            public void onFailure(FailureResponse failureResponse) {
                                super.onFailure(failureResponse);
				/* If pdf is not generated by an error then you will findout the reason behind it
				 * from this FailureResponse. */
                            }
			      @Override
                            public void onStartPDFGeneration() {
                                /*When PDF generation begins to start*/
                            }

                            @Override
                            public void onFinishPDFGeneration() {
                                /*When PDF generation is finished*/
                            }

                            @Override
                            public void showLog(String log) {
                                super.showLog(log);
				/*It shows logs of events inside the pdf generation process*/ 
                            }

                            @Override
                            public void onSuccess(SuccessResponse response) {
                                super.onSuccess(response);
				/* If PDF is generated successfully then you will find SuccessResponse 
				 * which holds the PdfDocument,File and path (where generated pdf is stored)*/
				
                            }
                        });
```

### From view IDs :

```java
    PdfGenerator.getBuilder()
                        .setContext(context)
                        .fromViewIDSource()
                        .fromViewID(activity,R.id.tv_print_area,R.id.tv_print_area)
			/* "fromViewID()" takes array of view ids those MUST BE and MUST BE contained in the inserted "activity" .
			 * You can also invoke "fromViewIDList()" method here which takes list of view ids instead of array. */
                        .setCustomPageSize(3000,3000)
			/* Here I used ".setCustomPageSize(3000,3000)" to set custom page size.*/
                        .setFileName("Test-PDF")
                        .setFolderName("Test-PDF-folder")
                        .openPDFafterGeneration(true)
                        .build(new PdfGeneratorListener() {
                            @Override
                            public void onFailure(FailureResponse failureResponse) {
                                super.onFailure(failureResponse);
                            }
			    
			       @Override
                            public void onStartPDFGeneration() {
                                /*When PDF generation begins to start*/
                            }

                            @Override
                            public void onFinishPDFGeneration() {
                                /*When PDF generation is finished*/
                            }

                            @Override
                            public void showLog(String log) {
                                super.showLog(log);
                            }

                            @Override
                            public void onSuccess(SuccessResponse response) {
                                super.onSuccess(response);
                            }
                        });
```

### From views:

```java 

PdfGenerator.getBuilder()
                        .setContext(MainActivity.this)
                        .fromViewSource()
                        .fromView(view) 
			/* "fromView()" takes array of view. You can also invoke "fromViewList()" method here
			 * which takes list of view instead of array. */
                        .setCustomPageSize(3000,3000)
                        .setFileName("Test-PDF")
                        .setFolderName("Test-PDF-folder")
                        .openPDFafterGeneration(true)
                        .build(new PdfGeneratorListener() {
                            @Override
                            public void onFailure(FailureResponse failureResponse) {
                                super.onFailure(failureResponse);
                            }

                            @Override
                            public void showLog(String log) {
                                super.showLog(log);
                            }

                            @Override
                            public void onStartPDFGeneration() {
                                /*When PDF generation begins to start*/
                            }

                            @Override
                            public void onFinishPDFGeneration() {
                                /*When PDF generation is finished*/ 
                            }
			    
                            @Override
                            public void onSuccess(SuccessResponse response) {
                                super.onSuccess(response);
                            }
                        });
```	

### Multi-paged PDF creation:
Users of the library, sometimes have doubts that how to create multi-paged PDF. Though I mentioned it above but I need to show it again for more clearance.
You can insert multiple xml or views object even view id in the parameter of the following methods to create multi-paged pdf: 


If you want create multi-paged pdf from xmls-

`.fromLayoutXML(R.layout.layout_1,R.layout.layout_2)`

 If you want create multi-paged pdf from view ids -
 
`.fromViewID(activity,R.id.viewId1,R.id.viewId2)`

 If you want create multi-paged pdf from views-
 
`.fromViewID(view1,view1)`


So if you find any trouble,then you are also welcomed again to knock me.Thank you so much. 
		

[![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/colored.png)](#templates)

<p>
  <a href="https://www.linkedin.com/in/gk-mohammad-emon-0301b7104" rel="nofollow noreferrer">
    <img src="https://i.stack.imgur.com/gVE0j.png" alt="linkedin"> LinkedIn
  </a> &nbsp; 
  <a href="emon.info2013@gmail.com">
   <img width="20" src="https://user-images.githubusercontent.com/5141132/50740364-7ea80880-1217-11e9-8faf-2348e31beedd.png" alt="inbox"> Inbox
  </a>
</p>

#### Logo credit: [kirillmazin](https://www.behance.net/kirillmazin)

## ➤ License

The source code is licensed under the [Apache License 2.0](https://github.com/Gkemon/XML-to-PDF-generator/blob/master/LICENSE). 


[![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/colored.png)](#license)


