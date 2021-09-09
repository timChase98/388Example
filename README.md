# ECE 388 Board Submission Standards

## Directory Layout
In the base Directory should be your Kicad project files and a directory called "renders" which contains the output files from your project. If you want to also version control your firmware (which you probably should) you can have a folder called "software" or "firmware" to manage code.  You must also add the gitignore from this repo.  

Your repo should be well maintained and updated regularly.  I should not just see a single commit titled "done".  You should be making frequent commits as you make changes to the status of your project.  You should also regularly push.  

## Submissions
Submissions should be in the form of GitHub Releases.  When a deadline comes around whatever the latest release on your repo is will be taken as your submission.  You should not email me submissions, email submissions will not be graded.  

Documentation on how to create a release can be found [HERE](https://docs.github.com/en/free-pro-team@latest/github/administering-a-repository/managing-releases-in-a-repository).

#### Schematics Submission
You will create a release called "Schematic Submission"

ERC must be run on all schematic before submission.  ERC errors will not only make your board not work, it will also make your design get rejected.  Schematics should be submitted as a PDF located in the "renders" folder.  To get Kicad to produce a PDF of your schematic select the plotter icon from the top menu and select the following settings.  

![schematicToPDF](/readmeImg/schematic.png)

It's important that if you have more than one page that you select to export all pages.

#### BOM Submission
You will create a release titled "BOM Submission"

We will be using [LCSC](https://lcsc.com) as out preferred supplier.  As such, all parts should be sourceable from LCSC unless previously discussed with myself.  Once submitted each group will meet with me for a Bill Of Materials (BOM) review.  BOM's should be exported from Kicad. To do this in Eeschema go to Tools -> Generate Bill Of Materials and select bom2grouped_csv.  

![bom](/readmeImg/bom.png)

After Kicad generates a BOM file you need to open it in a CSV editor of your choice, excel, open office, atom if your a cool kid, vscode if you're a nerd, and patch in the additional data needed to submit.  This includes price breakdowns, LCSC part numbers and links.  An example is provided in this repository.  If a part is not available from LCSC and you have discussed this with me you can enter data into the DigiKey fields, otherwise they are unnecessary.  Note price breakdowns are for the cost of 1 part at the listed quantity, not the extended price.  

**BOMs That do not meet the format specification will be rejected** This means they must have all of the correct columns, in the correct order, with correct data in them, and be in **CSV** format.  

**All parts necessary for production of you board must be on the BOM** this included displays, connectors, wiring, etc.  If you need it for your board to be functional it needs to be on the BOM. Components that are not physical parts, ex mounting holes, fiducials, etc, should not be included.  

**We are ordering parts from LCSC.  BOMs that do not have LSCS part numbers will be rejected**


#### Board Layout
It is important that the first thing you do when you start to layout your board is to setup your DRCs.  DRCs are the minimum checks you can do to make sure your board will have the possibility of being manufacturable.  They do not however verify your board will work correctly.  

We will be using JLCPCB's prototyping service for board production.  JLCPCB's design minimum design rules are located [HERE](https://jlcpcb.com/capabilities/Capabilities). **Some of these rules are different for different board configurations** unless you have specifically discussed with me your board will be 2 layer 1oz copper on 1.6mm FR-4.  Note these are minimums, not recommend.  You should use Kicad's built-in circuit board calculator to come up with minimum for high power or critical traces.  
All of these things need to be configured in the board setup dialog accessible via File -> Board Setup
It is also important to take note of silkscreen (called legend on the JLCPCB website) minimums.  A lot of standard libraries come with small text sizes and will need to be increased to pass DRC.  This can be done by setting the text properties in the Board Setup dialog.

![silkFix](/readmeImg/silkDRC.png)

Then going to Edit -> Text and Graphics properties and settings the following settings

![silkFix](/readmeImg/silkFix.png)

Additionally it can be useful to have the help of the interactive router.  This is entirely up to personal preference, my preferred settings are shown below.  This dialog is accessible via the Route -> Interactive Router Settings menu.

![routerSettings](/readmeImg/routeSettings.png)

Periodically while  laying out your board you should run a DRC to verify there are no manufacturing issues. It is sometimes ok to wave DRC errors as Approved.  If there is an error that you believe should be waved discuss this with Dr. Viall or myself before continuing.


To verify you read this put a text file in the Renders folder titled "Verification.txt" that contains the line "No Green M&M's were harmed in the production of this board" and nothing else.  

#### Board Submission
You will create a release called "Gerber Submission"

DRC must be run on your board prior to submitting.  Any unapproved DRC errors will result in your design being rejected.  
**Boards with critical DRC errors are unmanufacturable**

**Boards must be clearly marked with identifying information** This includes the product name, Revision, Date, Lead layout engineer, all group members names, and the link to the project GitHub.  An Example from a Seinor Design project is included below.  

![board](/readmeImg/renderedBoard.png)

**Boards must have Fiducials for automated assembly.** Submissions that do not have 1mm fiducials in the bottom left (FID1), Top Right (FID2), and Top Left (FID3) will be rejected. Note the ordering of the three fiducials is important for automated assembly. The area around fiducials should be clear of components that may interfere with automatic recognition (i.e. mounting holes, pin headers etc.) for at least 3mm from any edge of the copper center.  

Boards will be submitted in a folder containing gerber files produced with the provided CAM files.  To Load the CAM file open the CAM Processor and click the LOAD button.  The output of the CAM processor should be set to the renders folder.  

Directions to generate Gerber Files can be found [HERE](https://support.jlcpcb.com/article/149-how-to-generate-gerber-and-drill-files-in-kicad)

#### Board Population

In order to get a board assembled through the automated assembly process you must submit a finalized BOM that includes quantities and UUIDs from the stock sheet [HERE](https://docs.google.com/spreadsheets/d/1WtOakf2sV2Z24B9SvWYXxpJuLNhJUgvYpcEkdbbXuQU/edit#gid=0) and designators.  If a component is being sourced by you rather than a part that was ordered from the BOM you should put a "Y" in the self sourced column.  This file should only reflect components that need to be populated on the board.  i.e. resistors, caps, ICs, not mounting holes or solder jumpers.  An example of this is attached can be seen in this repo.  It should be named yourProjectName_assembly.csv and be in the base directory of your project when you create an assembly release.  Once you have submitted this file and your Kicad project files are in the repo you can schedule an appointment to get your board assembled.  


##Feedback

Feedback will be provided via Github Issues.  Changes that need to be made will be listed as a series of checkboxes on an issue.  These boxes should be checked off as they are completed.  You should have all of the boxes check before closing the issue to notify me that your submission needs to be revaluated.  Any discussion about should be done on the issue page.  

I can not recommend strongly enough that you have everything in as early as possible.  Your designs will likely get rejected the first time and you need time to be able to get a manufacturable board in before the deadline to order.  
