# Atualizando um arquivo SCORM

Agora vamos ver os arquivos que serão necessário atualizar com os dados do curso para que o SCORM funcione e esses arquivos possam ser lidos pelo LMS.

## imsmanifest.xml

O primeiro deles é o **imsmanifest.xml** que vai conter o seguinte conteúdo:

```xml
<?xml version="1.0" standalone="no" ?>
<manifest identifier="RusticiSoftwareSCORMDriverTemplate" version="1.3"
          xmlns="http://www.imsglobal.org/xsd/imscp_v1p1"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:adlcp="http://www.adlnet.org/xsd/adlcp_v1p3"
          xmlns:adlseq="http://www.adlnet.org/xsd/adlseq_v1p3"
          xmlns:adlnav="http://www.adlnet.org/xsd/adlnav_v1p3"
          xmlns:imsss="http://www.imsglobal.org/xsd/imsss"
          xsi:schemaLocation="http://www.imsglobal.org/xsd/imscp_v1p1 imscp_v1p1.xsd
                              http://www.adlnet.org/xsd/adlcp_v1p3 adlcp_v1p3.xsd
                              http://www.adlnet.org/xsd/adlseq_v1p3 adlseq_v1p3.xsd
                              http://www.adlnet.org/xsd/adlnav_v1p3 adlnav_v1p3.xsd
                              http://www.imsglobal.org/xsd/imsss imsss_v1p0.xsd">
     <metadata>
		<schema>ADL SCORM</schema>
		<schemaversion>2004 4th Edition</schemaversion>
		<adlcp:location>metadata.xml</adlcp:location>
	</metadata>
	<organizations default="B0">
		<organization identifier="B0" adlseq:objectivesGlobalToSystem="false">
			<!--****** Title ******-->
			<title>Course Title</title>
			<item identifier="i1" identifierref="r1" isvisible="true">
				<!--****** Title ******-->

				<title>Course Title</title>

				<imsss:sequencing>
					<imsss:objectives>
					        <imsss:primaryObjective objectiveID="PRIMARYOBJ"/>
					</imsss:objectives>
                    <imsss:deliveryControls tracked="true" completionSetByContent="true" objectiveSetByContent="true"/>
				</imsss:sequencing>
			</item>
			<metadata>
				<adlcp:location>metadata.xml</adlcp:location>
			</metadata>			
			<imsss:sequencing>
				<imsss:controlMode choice="true" flow="true"/>
                <imsss:rollupRules>
                    <imsss:rollupRule childActivitySet="all">
                        <imsss:rollupConditions>
                            <imsss:rollupCondition condition="satisfied"/>
                        </imsss:rollupConditions>
                        <imsss:rollupAction action="satisfied"/>
                    </imsss:rollupRule>
                    <imsss:rollupRule childActivitySet="all">
                        <imsss:rollupConditions>
                            <imsss:rollupCondition operator="not" condition="satisfied"/>
                        </imsss:rollupConditions>
                        <imsss:rollupAction action="notSatisfied"/>
                    </imsss:rollupRule>
                    <imsss:rollupRule childActivitySet="all">
                        <imsss:rollupConditions>
                            <imsss:rollupCondition condition="completed"/>
                        </imsss:rollupConditions>
                        <imsss:rollupAction action="completed"/>
                    </imsss:rollupRule>
                    <imsss:rollupRule childActivitySet="all">
                        <imsss:rollupConditions>
                            <imsss:rollupCondition operator="not" condition="completed"/>
                        </imsss:rollupConditions>
                        <imsss:rollupAction action="incomplete"/>
                    </imsss:rollupRule>
                </imsss:rollupRules>
			</imsss:sequencing>
		</organization>
	</organizations>
	<resources>
		<resource identifier="r1" type="webcontent" adlcp:scormType="sco" href="scormdriver/indexAPI.html">
			 <file href="scormdriver/indexAPI.html" />
				<file href="LICENSE.txt" />
	            <file href="readme.txt" /> 
	 			<file href="scormcontent/index.html" /> 
	 			<file href="scormdriver/AICCComm.html" /> 
	 			<file href="scormdriver/auto-scripts/AutoBookmark.js" /> 
	 			<file href="scormdriver/auto-scripts/AutoCompleteSCO.js" /> 
	 			<file href="scormdriver/auto-scripts/CourseExit.js" /> 
	 			<file href="scormdriver/blank.html" /> 
	 			<file href="scormdriver/goodbye.html" /> 
	 			<file href="scormdriver/scormdriver.js" />
				<file href="scormdriver/browsersniff.js" />
		</resource>
	</resources>
</manifest>
```

1. Logo na primeira linha podemos ver **identifier** que será o ID do curso.
2. Abaixo teremos a tag 
```html
 <title>Course Title</title>
``` 
que nada mais é que o título que será mostrado para o usuário, título do curso, devemos atualizar ambas as tags title sendo o primeiro o título principal. 

## metadata.xml

O segundo arquivo que vamos trabalhar é o **metadata.xml** que irá conter o seguinte conteúdo:

```xml
<?xml version="1.0"?>
<lom xmlns="http://ltsc.ieee.org/xsd/LOM"
     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
     xmlns:pkgprop="http://www.scorm.com/xsd/ScormEnginePackageProperties"
     xsi:schemaLocation="http://ltsc.ieee.org/xsd/LOM lomLoose.xsd 
                         http://www.scorm.com/xsd/ScormEnginePackageProperties ScormEnginePackageProperties.xsd">
    <general>

        <!-- Repace XXXXXXXX with Manifest->Course.Identifier field value. Only include valid URI characters. If no value specifed, use a GUID.-->
        <identifier>
            <catalog>URI</catalog>
            <entry>com.company.product.XXXXXXXX</entry>
        </identifier>

        <!-- Replce with Manifest->Course.Title field value. If that doesn't exist use Project Information->Project Name. If nothing specifed there use something generic like "Adobe Captivate Course" -->
        <!-- For every instance of "<string language="en-US">" if you know the language of the user, use that language code. If you do not know the language code then omit all instances of "language="en-US"" -->
        <title>
            <string language="en-US">Golf Explained</string>
        </title>

        <!-- If you know the locale, enter it here, if not, remove this node-->
        <language>en</language>

        <!-- Manifest->Course.Description. If that doesn't exist, replace with Project Information-> Description. If that is empty just remove the node.-->
        <description>
            <string language="en-US">A high level overview of the sport of golf. This course describes how to play golf, how to use a golf handicap, the etiquette of golfing and how to have fun while playing.</string>
        </description>

    </general>

    <lifeCycle>
        <!-- Use Manifest->Course.Version. If that doesn't exist, either defaul to a value like "1" or remove the verion note entirely -->
        <version>
            <string language="en-US">1.0</string>
        </version>

        <contribute>
            <role>
                <source>LOMv1.0</source>
                <value>author</value>
            </role>
            <entity>
                <![CDATA[BEGIN:VCARD
VERSION:2.1
FN: Put ProjectInformation->Author here. if not filled in use ProjectInformation->Company, if nothing there, omit this line
ORG: Put ProjectInformation->Company here, if not filled in, omit this line
EMAIL;PREF;INTERNET: Put Projet Informatin->Email here, if not filled in, omit this line
URL:  Put Projet Informatin->Website here, if not filled in, omit this line
END:VCARD]]>
            </entity>
            <date>
                <dateTime>2009-01-23</dateTime>
                <!-- Replace with the current time stamp when exporting from Captivate -->
                <description>
                    <string language="en-US">This is the date this course was published from Adobe Captivate.</string>
                </description>
            </date>
        </contribute>

        <contribute>
            <role>
                <source>LOMv1.0</source>
                <value>publisher</value>
            </role>
            <entity>
                <![CDATA[BEGIN:VCARD
VERSION:2.1
FN:Adobe Captivate
NOTE: version XXX       <!-- Put your actual version number in here each relase -->
URL: http://www.adobe.com/products/captivate.html
END:VCARD]]>
            </entity>
        </contribute>

        <contribute>
            <role>
                <source>LOMv1.0</source>
                <value>technical implementer</value>
            </role>
            <entity>
                <![CDATA[BEGIN:VCARD 
VERSION:2.1 
FN:SCORM Driver
ORG:Rustici Software,LLC
TEL;WORK;VOICE:(866)49-SCORM 
ADR;WORK:;;3326 Aspen Grove Dr Ste 304;Franklin;TN;37067;United States of America 
EMAIL;PREF;INTERNET:info@scorm.com 
URL: http://scorm.com
END:VCARD]]>
            </entity>
        </contribute>
        
    </lifeCycle>

    <technical>

        <format>text/html</format>
        <format>application/x-javascript</format>
        <format>application/x-shockwave-flash</format>
        <format>text/css</format>

        <size>516096</size>
        <!-- If you know the actual size of the output file include it here (in bytes). If not, just omit this node.-->

        <!-- Use the value displayed at the bottom of Project Information->Time here. This duration is the time the media takes to play through. -->
        <duration>
            <duration>PT10M</duration>
            <description>
                <string language="en-us">Time it will take to watch this presentation directly from start to finish.</string>
            </description>
        </duration>
        <pkgprop:ScormEnginePackageProperties xmlns="http://www.scorm.com/xsd/ScormEnginePackageProperties">
            <appearence>
                <displayStage>
                    <desired>
                        <!-- Replace with target width and height of movie. (From Project Information -> Resolution -->
                        <width>750</width>
                        <height>550</height>
                        <fullscreen>no</fullscreen>
                    </desired>
                    <required>
                        <width>0</width>
                        <height>0</height>
                        <fullscreen>no</fullscreen>
                    </required>
                </displayStage>
            </appearence>
            <behavior>
                <alwaysFlowToFirstSco>yes</alwaysFlowToFirstSco>
                <rollupEmptySetToUnknown>yes</rollupEmptySetToUnknown>
            </behavior>
        </pkgprop:ScormEnginePackageProperties>
    </technical>

    <educational>
        <!-- Use the value from Manifest-> Duration here. This is the time it will take for a typical learner to progress through the course, fully experiencing it.-->
        <typicalLearningTime>
            <duration>PT10M</duration>
            <description>
                <string language="en-us">Time it will typically take for a learner to complete this course.</string>
            </description>
        </typicalLearningTime>

        <!-- Manifest->Course.Description. If that doesn't exist, replace with Project Information-> Description  (same as description above)-->
        <description>
            <string>This course should be used to provide people with a new interest in golf an overview of the game. It does not provide instruction on how to swing a club or any other athletic advice. It is purely an overview of the concepts of the game.</string>
        </description>

        <!-- If you know the locale, enter it here, if not, remove this node (same as language above)-->
        <language>en-us</language>

    </educational>

    <rights>

        <copyrightAndOtherRestrictions>
            <source>LOMv1.0</source>
            <value>yes</value>
        </copyrightAndOtherRestrictions>

        <!-- Enter Project Information->Copyright here. If blank, omit the description. -->
        <description>
            <string>This content may be freely distributed subject to the Creative Commons Attribution 3.0 United States License.</string>
        </description>

    </rights>
</lom>

```

Aqui o que mais nos interessa é notar as tags **title**, **language** e **description**. que tem como exemplo um curso de golf, é necessário mudarmos o title para o título do nosso curso, de preferência para o mesmo que foi usado nos arquivos anteriores, em decription a descrição do curso e em language a língua local em que esses conteúdos serão consumidos.

Esses serão os dois únicos arquivos que vamos a príncipio precisar mudar para que nosso conteúdo possa ser lido.
