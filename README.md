# HUSA

## DOS_XX_LAGER_MARCH Email Template - Technical review of corrections and feedback

### Issues flagged in initial test send

	- [1] The following buttons are currently clicking to our website’s beers&recipes. But they should click to here: www.DosEquis.com/XXHoopsContest  
		Click to Enter
		Upload your photo
		#XXHoops #contest
		
	- [2] The following buttons are not displaying correctly when I open the email on desktop as seen on the screenshot attached.
		Upload your photo
		#XXHoops #contest
		![image](https://user-images.githubusercontent.com/102308411/159946878-0c87eb85-b06b-40a7-a86d-f6701aef432e.png)
		
	- [3] The Ranch Water in the product section is displaying a little off on desktop.
		![image](https://user-images.githubusercontent.com/102308411/159946960-c91ffdf8-9659-4e60-8719-5fbb1341c480.png)
		
	- [4] The Steps are displaying incorrectly on mobile. It should go: Step 1 + image, Step 2 + image and then step 3 + image. 
		But right now the image for step 2 is displaying together with Step 1.
		![image](https://user-images.githubusercontent.com/102308411/159947543-63d926ef-2426-432e-8551-eb644d18821a.png)
		
	- [5] The product description on mobile is displaying below the division line/bar so it seems like the description belongs to the product below it. 
		Like for example, the description “ When you’re thirsty for something more” belongs to Lager, 
		so it should be above the line to avoid confusion thinking that it’s describing Lime and Salt. (screenshot attached)
	
### Additional 
	- [6] Part of the email content gets cut off in the preview panel of the web client in Outlook. Happen on windows resize under circa 600px width
	
### Environment for reproducing 

Issues [1], [2] and [3] occured in <b>Microsoft Outlook</b>, possibly a old version of the desktop client

Issues [4] and [5] occurred on any mobile mail client

Issue [6] <b>Microsoft Outlook</b> web client

### Causes

Issues [1], [2] and [3] were caused by [dbo] conditional statements, specific code rendered by Microsoft Word, the engine used by Microsoft Outlook, that were copied from previous templates and have not been updated accordingly to the new layout.

Issues [4] and [5] were caused by a lack of a mobile aware design in the template, 
    [4] the order of the section was: <br>
                    Button         Image <br>
                    Image          Button <br>
                    Button         Image <br>
    When this 2 columns layout was displayed in single column on mobile it went: <br>
                    Button<br>
                    Image<br>
                    Image<br>
                    Button<br>
                    Button<br>
                    Image<br>
    [5] mobile simply needed a different border position

Issue [6] is a common issue caused by the Preview Pane in Outlook not triggering specific CSS media rules even when getting under a certain width.

### Fixes

[1] Simple update of the anchor tags in the [dbo] comments

[2] center alignement and wider buttons

    Original code: 
												
	<!--[if mso]><table width="100%" cellpadding="0" cellspacing="0" border="0" style="border-spacing: 0; border-collapse: collapse; mso-table-lspace:0pt; mso-table-rspace:0pt;"><tr><td style="padding-top: 10px; padding-right: 10px; padding-bottom: 10px; padding-left: 10px" align="left"><v:roundrect xmlns:v="urn:schemas-microsoft-com:vml" xmlns:w="urn:schemas-microsoft-com:office:word" href="https://dosequis.com/beers-and-recipes/mint-chelada/" style="height:21.75pt;width:94.5pt;v-text-anchor:middle;" arcsize="14%" stroke="false" fillcolor="#e51f3d"><w:anchorlock/><v:textbox inset="0,0,0,0"><center style="color:#ffffff; font-family:Arial, sans-serif; font-size:10px"><![endif]-->
												
		
    Updated code: 

												
	<!--[if mso]><table width="100%" cellpadding="0" cellspacing="0" border="0" style="border-spacing: 0; border-collapse: collapse; mso-table-lspace:0pt; mso-table-rspace:0pt;"><tr><td style="padding-top: 10px; padding-right: 10px; padding-bottom: 10px; padding-left: 10px" align="center"><v:roundrect xmlns:v="urn:schemas-microsoft-com:vml" xmlns:w="urn:schemas-microsoft-com:office:word" href="https://dosequis.com/xxhoopscontest/?emailhash={{emailhash}}" style="height:21.75pt;width:130.5pt;v-text-anchor:middle;" arcsize="14%" stroke="false" fillcolor="#e51f3d"><w:anchorlock/><v:textbox inset="0,0,0,0"><center style="color:#ffffff; font-family:Arial, sans-serif; font-size:10px"><![endif]-->
												
[3] Similarly, the [dbo] comment was not updated from the previous template, adjusted padding and font size 


	<!--[if mso]><table width="100%" cellpadding="0" cellspacing="0" border="0"><tr><td style="padding-right: 10px; padding-left: 10px; padding-top: 10px; padding-bottom: 10px; font-family: Arial, sans-serif"><![endif]-->
												
	<!--[if mso]><table width="100%" cellpadding="0" cellspacing="0" border="0"><tr><td style="padding-right: 5px; padding-left: 5px; padding-top: 10px; padding-bottom: 10px; font-family: Arial, sans-serif"><![endif]-->

[4] Steps in second row readjusted to Button Image but displayed in dir="rtl" on desktop.


    <div dir="rtl" style="border-collapse: collapse;display: table;width: 100%;background-color:#f6f6f6;">
								
        <div class="col num6" style="display: table-cell; vertical-align: top; max-width: 320px; min-width: 246px; width: 250px;">
		    <div class="button-container" align="center" style="padding-top:10px;padding-right:10px;padding-bottom:10px;padding-left:25px;"> </div>
	    </div>
								
        <div class="col num6" style="display: table-cell; vertical-align: top; max-width: 320px; min-width: 246px; width: 250px; position: sticky; left: 0">
            <div class="img-container center autowidth" align="center" style="padding-right: 0px;padding-left: 0px;"></div>
        </div>

	</div>

[5] Added specific mobile borders hidden on dekstop

    <table class="divider desktop_hide" border="0" cellpadding="0" cellspacing="0" width="100%" style="table-layout: fixed; vertical-align: top; border-spacing: 0; border-collapse: collapse; mso-table-lspace: 0pt; mso-table-rspace: 0pt; min-width: 100%; -ms-text-size-adjust: 100%; -webkit-text-size-adjust: 100%;" role="presentation" valign="top"></table>

[6] This is a very finge issue, triggered in very specific scenarios and not fully compromising the reader's experience, but it doesn't allow for easy access to the full email body. It was just noticed towards the end of the troubleshooting and required a re-design of the template to fix, so It's been put in hold for the moment. A possible solution is to think of a <u>fluid</u> more than responsive design, create a layout that scales well under with diminishing widths rather that using CSS rules for mobile.

## Conclusions and suggestions

Most of these issues were cause by forgotten [dbo] statements inside the source code. These statements, recognised by the fact that they're commented out, are extremely important for the email rendering on certain email clients, so please be sure they're properly updated when working on an imported email template. Issues [4] and [5] were present in multiple past emails, they flew under the radar so far but it would be good to keep a mobile aware attitude while creating templates, do a lot of testing and please prepare documentation for the client to preview both a Desktop view and a Mobile view of the email.
     
