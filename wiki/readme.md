From: <https://wiki.to.infn.it/vlsi/workbook/analog/cdsenv>

###### Cadence environment and setup files

\[ \_\_[Home](vlsi:home "wikilink")\_\_ \] \[ \_\_[Back to
index](vlsi:workbook:analog#contents "wikilink")\_\_ \]

## Contents

`  * `[`Introduction`](vlsi:workbook:analog:cdsenv#introduction "wikilink")  
`  * `[`Reference documentation`](vlsi:workbook:analog:cdsenv#reference_documentation "wikilink")  
`  * `[`Sample files`](vlsi:workbook:analog:cdsenv#sample_files "wikilink")  
`  * `[`.cadence directories`](vlsi:workbook:analog:cdsenv#.cadence_directories "wikilink")  
`  * `[`.cdsenv and .cdsinit initialization files`](vlsi:workbook:analog:cdsenv#.cdsenv_and_.cdsinit_initialization_files "wikilink")  
`  * `[`.cdsinit_tech`](vlsi:workbook:analog:cdsenv#.cdsinit_tech "wikilink")  
`  * `[`libInit.il`](vlsi:workbook:analog:cdsenv#libinit.il "wikilink")  
`  * `[`CDS.log`](vlsi:workbook:analog:cdsenv#cds.log "wikilink")  
`  * `[`.simrc`](vlsi:workbook:analog:cdsenv#.simrc "wikilink")  
`  * `[`.cdsplotinit`](vlsi:workbook:analog:cdsenv#.cdsplotinit "wikilink")  
`  * `[`cds.lib library definition file`](vlsi:workbook:analog:cdsenv#cds.lib_library_definition_file "wikilink")  
`  * `[`Simulation results and saved states directories`](vlsi:workbook:analog:cdsenv#simulation_results_and_saved_states_directories "wikilink")  
`  * `[`display.drf`](vlsi:workbook:analog:cdsenv#display.drf "wikilink")  
`  * `[`Bindkeys`](vlsi:workbook:analog:cdsenv#bindkeys "wikilink")  
`  * `[`Some customization examples`](vlsi:workbook:analog:cdsenv#some_customization_examples "wikilink")

-   -   Keywords:\*\*

##### Introduction

The key to succesfully run the different VLSI tools is to know the most
important configuration files and how the system administrator has
planned them to be used. A basic knowledge about these files is
fundamental in helping users to fix the most common problems by
themselves. Keep in mind that with a standard VLSI account you have
\*\*write privileges\*\* only inside your home directory and in the
system temporary */tmp*. Therefore each user should exploit as much as
possible customizations which can be made inside the local area. In
general \*\*keep backups\*\* of various configuration files (e.g. *cp
filename filename.old*) each time before making changes.

and to Cadence's design tools All the examples will be referred to the
\*\*Cadence IC 6.1.x\*\* (Virtuoso) platform. The full path for the
referenced *$IC_DIR* environment variable is */usr/cadence/IC_6.1.x*,
corresponding to the top Cadence IC 6.1.x installation directory (the
last software release is 6.1.5). Use the *setenv* command:

`setenv IC_DIR /usr/cadence/IC_6.1.5`

##### Reference documentation

For detailed information about the Cadence IC general configuration
please refer to the //Virtuoso Software Licensing and Configuration User
Guide//. The relative pdf file is

*/usr/cadence/IC_6.1.x/doc/dfIIconfig/dfIIconfig.pdf*

##### Sample files

A well commented set of \*\*sample files\*\* comes with the Cadence IC
installation itself. Sample \*\*home directory\*\* setup files (e.g.
*.cshrc* and *.cdsinit*) can be found in the
*$IC_DIR/tools/dfII/cdsuser* directory, whereas \*\*working
directory\*\* templates (e.g. *.cdsenv* and *cds.lib*) have been placed
in *$IC_DIR/tools/dfII/samples*:

`ls -l $IC_DIR/tools/dfII/cdsuser ls -l $IC_DIR/tools/dfII/samples`

\\ These files can be copied to a your local area and then customized.
We suggest to create in your *~/scratch* directory a new directory to
contain the original templates, e.g.

`cd ~/scratch mkdir sample.files`

##### .cadence directories

The first time you run a Cadence tools (e.g. *virtuoso*) a *./.cadence*
hidden directory is automatically created in your working directory and
a further *~/.cadence* is created in the home directory. These are may
be used to customize the Cadence environment.

##### .cdsenv and .cdsinit initialization files

In this section we introduce the most important set of initialization
files related to Cadence tools. We can distinguish between \*\*site\*\*
(global) and \*\*user\*\* (local) setup files. Site initialization files
are provided by the system administrator and are used to set up a common
environment for the various Cadence tools and for the chosen technology.
On the other hand, each user can \*\*customize\*\* the Cadence behavior
to fit his needs by using local initialization files. Of course
individual user settings override any global customization. We stress
again that each user should exploit as much as possible local
customizations.

The main Cadence initialization files are named *.cdsenv* and
*.cdsinit*. Depending on the system administrator setup, user *.cdsinit*
files may have a different name like *.cdsinit_personal*,
*.cdsinit_user* or *.cdsinit_local*. Both *.cdsenv* and *.cdsinit* are
used to define the Cadence environment, but with some differences.
*.cdsenv* files follow their own syntax and are used to set tool options
and user preferences. The *.cdsinit* files use SKILL syntax and
typically are used just to load further SKILL setup files into the
system (e.g. bindkeys files). The *.cdsenv* files are loaded before the
*.cdsinit* ones. Therefore settings defined in the *.cdsinit* files may
override settings placed in the *.cdsenv*. See also
//<http://www.edaboard.co.uk/cdsenv-and-cdsinit-t374951.html>//

*.cdsenv* files are loaded from different paths. Each tool has its own
default *.cdsenv* file, placed in
*$IC_DIR/tools/dfII/etc/tools/<application>/* directories (e.g.
*$IC_DIR/tools/dfII/etc/tools/schematic/.cdsenv* for //Virtuoso
Schematic Editor//). A site *.cdsenv* could be put by the system
administrator in the *$IC_DIR/tools/dfII/local/* directory, which is the
\*\*site customization directory\*\*. In general this is a modified copy
of the sample *IC_DIR/tools/dfII/samples/.cdsenv* file which comes with
the Cadence IC installation. User customizations can be defined in a
local *~/.cdsenv* in your \*\*home directory\*\*. When you start a
Cadence session, if the *CDS_LOAD_ENV* environment variable is not set
the program loads \*\*all\*\* the above mentioned *.cdsenv* files in the
following sequence:

`  * `*`$IC_DIR/tools/dfII/etc/tools/`<application>`/.cdsenv`*

`  * `*`$IC_DIR/tools/dfII/local/.cdsenv`*` (site customizations)`

`  * `*`~/.cdsenv`*` (user customizations)`

Any value defined in the home *~/.cdsenv* overrides those previously
loaded. Please note that the default search mechanism for the *.cdsenv*
file does not look in the \*\*working directory\*\*. Hence a *./.cdsenv*
file placed in your working directory is not loaded by default. If you
want it to be loaded, you have to set the *CDS_LOAD_ENV* environment
variable equal to *addCWD* in your *.cshrc*:

`setenv CDS_LOAD_ENV addCWD`

\\ Alternatively you can put a

`envLoadFile("./.cdsenv")`

statement in the home *.cdsinit_personal* described below.

A working directory *./.cdsenv* is useful to define customizations
related to the specific technology you are working with (e.g. model
files, layout options etc). Make a local copy of the sample *.cdsenv*
file and use this template for your *~/.cdsenv* and *./.cdsenv*:

`cp $IC_DIR/tools/dfII/samples/.cdsenv ~/scratch/sample.files/cdsenv.sample`

\\ Before you start customizations read the entire file and the
comments. Use *more cdsenv.sample* or *less cdsenv.sample* to see the
file content. User preferences can be also automatically saved to a
*.cdsenv* file from Cadence itself, e.g. by using \*\*CIW =\> Options
=\> Save defaults\*\*.

FIXME (screenshot!)

For more information about *.cdsenv* see also
//<http://eda.engineering.wustl.edu/wiki/index.php/Cadence_Environment>//.

The loading procedure is slight different for the *.cdsinit* files. Only
the \*\*first\*\* *.cdsinit* file found during Cadence startup is
loaded, then the search stops and no more *.cdsinit* files would be
automatically loaded unless explicitely specified in the first one. The
first file encountered is the site *.cdinit* provided by the system
administrator and placed in the *$IC_DIR/tools/dfII/local/* directory.
This is a customized copy of the sample
*IC_DIR/tools/dfII/samples/local/cdsinit* site file which comes with the
Cadence IC installation. Then it's up to the site *.cdsinit* to load
user customization files, named *~/.cdsinit_personal* in the home
directory and *./.cdsinit_local* or *./.cdsinit* in the working
directory. The site *.cdsinit* also loads a \*\*technology-dependent\*\*
initialization file named *.cdsinit_tech* provided by the manufacturer,
which is usually placed in the main PDK installation directory. Inspect
the content of the site *.cdsinit*, e.g.

`more $IC_DIR/tools/dfII/local/.cdsinit`

and try to identify the various load statements for the above mentioned
files. The overall loading sequence is the following:

`  * `*`$IC_DIR/tools/dfII/local/.cdsinit`*` (site initialization file)`

`  * `*`~/.cdsinit_personal`*` (user customizations)`

`  * `*`./.cdsinit_local`*` or `*`./.cdsinit`*` (user customizations)`

Please note that a *~/.cdsinit* would not be loaded at all, unless
explicitely loaded by your *~/.cdsinit_personal*. A user *.cdsinit*
sample file comes with the Cadence installation in the
*$IC_DIR/tools/dfII/cdsuser/* directory. You can copy it to your local
scratch area and then customize it, as suggested for the *.cdsenv*
template:

`cp $IC_DIR/tools/dfII/cdsuser/.cdsinit ~/scratch/sample.files/cdsinit.sample`

\\ Remember that settings placed in *.cdsinit_personal* and
*.cdsinit_local* files may override the *.cdsenv* setup.

In general you can load in Cadence whatever initialization file you
want, but you have to explicitely include a *load()* statement in the
user *.cdsinit_personal* or *.cdsinit_local* files, e.g.

`when(isFile("/path/to/fileName") load("/path/to/fileName") )`

or simply type at the CIW command prompt

`load("/path/to/fileName")`

Posso specificare di non caricare nessun *cds.lib* at *virtuoso* startup
with the *-nocdsinit* option,

`virtuoso -nocdsinit`

##### .cdsinit_tech

*.cdsinit_tech* represents the main \*\*technology initialization
file\*\* loaded during Cadence startup. The default template is provided
by the manufacturer and comes with the PDK installation. Further
customizations can be done by the system administrator reflecting the
system configuration. As mentioned above the *.cdsinit_tech* is
explicitely loaded by the site *.cdsinit* file, in which you can find
the following directives:

`processdir = getShellEnvVar("ProcessPath") ... loadi( strcat(processdir "/.cdsinit_tech") )`

\\ The hard path of the *.cdsinit_tech* file varies with the technology.
If you want to know the exact location move to the main PDK installation
directory and use the *find* command, e.g.

`cd /path/to/PDK/installatio/directory find ./ -name .cdsinit_tech`

\\ Usually a *.cdsinit_tech* file sets some default user preferences and
could load further technology-related SKILL scripts or context files
(SKILL code compiled into binary files). In general available context
files have been encrypted by the manufacturer.

If your technology supports Mentor's \*\*Calibre\*\* verification tool
for design rule checks (DRC), layout versus schematic (LVS) etc. the
*.cdsinit_tech* should also load the main *calibre.skl* SKILL interface
which integrates Calibre menus in Cadence. Please check if your
*.cdsinit_tech* contains something like

`mgc_home=getShellEnvVar("MGC_HOME") ... load(strcat(mgc_home "/shared/pkgs/icv/tools/queryskl/calibre.skl"))`

\\ It could be useful to create a symbolic link to *.cdsinit_tech* in
your working directory:

`cd ~/scratch/`<tech_dir>` ln -s /path/to/.cdsinit_tech .cdsinit_tech`

##### libInit.il

Al di fuori di quello che interessa all'utente, solo per dire che
esiste.

Puo' caricare anche la definizione di Cadence technology-specific
\*\*custom menus\*\* which will be integrated in the Cadence graphical
front-ends. (typically in the form of context files, i.e. precompiled
SKILL code)

The *libInit.il* file is a SKILL script which is executed the first time
a \*\*library\*\* is opened.

Loads default technology \*\*model files\*\* and display resource file
*display.drf*

PDK utility menus, SKILL code and context files.

`cd /path/to/PDK/installation/directory find ./ -name libInit.il`

##### CDS.log

Log file

lo posso specificare anche at *virtuoso* startup

`virtuoso -log /path/to/filename`

e.g. put in a *logs* directory created in the working directory (*./*),

`virtuoso -log ./logs/filename.log`

Le default directories in cui salvare i log sono definiti in the
environment variable,

`setenv ????`

##### .simrc

This file is used for customizing simulation runs.

`cp $IC_DIR/tools/dfII/cdsuser/.simrc ~/scratch/sample.files/simrc.sample`

##### .cdsplotinit

cadence printing setup file, *$IC_DIR/tools/plot/.plotinit*

`cp $IC_DIR/tools/plot/.plotinit ~/scratch/sample.files/plotinit.sample`

##### cds.lib library definition file

The *cds.lib* is the \*\*libraries\*\* setup file.

The default Cadence DFII *cds.lib* file is
*$IC_DIR/tools/dfII/local/cds.lib*

`cd ~/scratch/`<tech_dir>` touch cds.lib`

If you are working with a particular \*\*technology\*\* you have to
include also the technology *cds.lib* usually located in the PDK
installation directory

<code>

1.  default Cadence IC cds.lib

INCLUDE $IC_DIR/tools/dfII/local/cds.lib

1.  technology cds.lib

INCLUDE /path/to/technology/cds.lib

1.  users libraries

DEFINE libName ~/scratch/<tech_dir>/lib/lbName DEFINE ... DEFINE ...
</code>

The Cadence Library Definition file (cds.lib) is located under your
Cadence installation directory. This is your library setup file A
default *cds.lib* file is located in

*<sub>$IC_DIR/tools/dfII/samples/cds.lib</sub>*

cds.lib example

<code>

1.  cds.lib skeleton

<!-- -->

1.  Standard Cadence libraries

INCLUDE $IC_DIR/tools/dfII/local/cds.lib ... ...

1.  technology libraries

INCLUDE /path/to/technology/specific/cds.lib

1.  custom libraries

DEFINE library_name /path/to/libary_name DEFINE .... /.../.../...
</code>

###### Simulation results and saved states directories

By default, all \*\*simulation data and results\*\* are stored in a
*~/simulation* directory automatically created in your home directory
the first time you run a simulation with Cadence IC. Similarly, Cadence
\*\*simulation states\*\* by default are saved in a *~/.artist_states*
hidden directoryautomatically created in your home directory.

To change these defaults, just use in your home *~/.cdsinit* or
*~/.cdsinit_personal* files the following directives

`envSetVal("asimenv.startup" "projectDir" 'string "/path/to/your/custom/simulation/results/directory") envSetVal("asimenv" "saveDir" 'string "/path/to/your/custom/simulation/states/directory")`

\\ You can type these statements at the CIW command prompt as well.

\\ See also

<http://www.cadence.com/Community/forums/p/17009/1179512.aspx>

##### display.drf

The \*\*display resource file\*\* defines necessary layout layers for a
specific technology. A good place to store the *display.drf* is the
working directory

all technologies have different *display.drf* files

`cd ~/scratch/`<tech_dir>` cp /path/to/technology/display.drf .`

\\ or simply create a symbolik link:

`cd ~/scratch/`<tech_dir>` ln -s /path/to/technology/display.drf display.drf`

-   -   CIW =\> Tools =\> Display Resource Manager...\*\* and choose
        //Merge//

For more details see the //Technology File and Display Resource File
User Guide// located in *$IC_DIR/doc/techfileuser/techfileuser.pdf*

##### Bindkeys

Bindkeys (hotkeys) in Cadence are \*\*keyboard shortcuts\*\* (both using
single keys or sequences of keys) or \*\*mouse actions\*\* (alone or in
combination with one modifier keys on the keyboard, typically *Shift*,
*Tab*, *Alt* and *Ctrl*) associated to some particular task or
functionality. Using bindkeys allow the designer to \*\*save time\*\*
avoiding search-and-click procedures, in particular during the shematic
entry phase and for layouting. Cadence's tools offer predefined sets of
bindkeys, whereas a technology could introduce its own bindkeys (which
may ovveride some Cadence's defaults). Of course each user is free to
define custom bindkeys to fit his needs.

Bindkeys are defined in SKILL (*.il*) files. Sample bindkeys for
//Virtuoso Schematic Editor// and //Virtuoso Layout Editor// comes with
the IC installation and can be found in
*$IC_DIR/tools/dfII/samples/local/schBindKeys.il* and
*$IC_DIR/tools/dfII/samples/local/leBindKeys.il* respectively. On the
other hand default bindkeys are automatically loaded at Cadence startup
from the *$IC_DIR/share/cdssetup/dfII/bindkeys/* directory (e.g.
*Schematics.il* and *Layout.il*). Actually sample files contain the same
bindkeys definition as given in the loaded files. Once Cadence opens you
can view currently set bindkeys through \*\*CIW =\> Options =\>
Bindkeys...\*\*.

If you plan to modify default bindkeys start making a local copy in your
*~/scratch* area of the sample files provided with the Cadence
installation, e.g.

`cd ~/scratch/ mkdir bindkeys cd bindkeys cp $IC_DIR/tools/dfII/samples/local/schBindKeys.il schBindKeys.il.default # for schematic bindkeys cp $IC_DIR/tools/dfII/samples/local/leBindKeys.il leBindKeys.il.default # for layout bindkeys`

Further sample files can be found in the
*$IC_DIR/tools/dfII/samples/local/* directory.

If you want to start with a 'vanilla' Cadence environment you can ensure
that default bindkeys are always loaded at Cadence startup. Simply add
in your home *~/.cdsinit_personal* the following lines:

`printf("Loading standard bindkeys. \n") load("~/scratch/bindkeys/schBindKeys.il.default") load("~/scratch/bindkeys/leBindKeys.il.default")`

or equivalently

`printf("Loading standard bindkeys. \n") load(prependInstallPath "samples/local/schBindKey.il") load(prependInstallPath "samples/local/leBindKeys.il")`

\\ Custom bindkeys for a particular technology should be placed in the
working directory *./.cdsinit* or *./.cdsinit_local*. If you would like
to create your own bindkeys, you must first know the SKILL function of
the command you are trying to bind. If you don't know the SKILL function
you can find it looking at output log messages registered in the CIW or
in *CDS.log* file. Only default bindkeys will be mentioned in the
WorkBook.

For more information about bindkeys see also

<http://cadence.wikispaces.com/Bindkeys> \\
<https://secure.engr.oregonstate.edu/wiki/ams/index.php/Cadence/TipsAndTricks>

###### Customization examples

The general *.cdsenv* syntax is like

<code> tool option type value <code>

e.g.

`layout gravityOn boolean nil`

The same otion defined in a *.cdsinit* file requires the usage of a
specific SKILL function,

`leSetEnv("gravityOn" nil)`

\\

-   -   Simulation options\*\*\\

If you want to change the default directory '~/.artist_states' used to
store simulation results

`asimenv.startup data string "~/cadence/`<tech_dir>`/data"`

To set the default simulator, e.g. as Spectre, enter the following
environment variable

`in your .cdsenv or .cdsinit file.`  
`Syntax to set the default simulator in the .cdsenv`

`asimenv.startup simulator string "spectre"`

Syntax to set the default simualtor in the .cdsinit
`envSetVal("asimenv.startup" "simulator" 'string "spectre")`

Definire il model path:

`spectre.envOpts modelPath string "/path/to/model/file.scs;section"`

See also //<http://cadence.wikispaces.com/simulatoroptions>//.

\\

-   -   Layout options\*\*\\

`layout snapMode string "anyAngle" layout`

\\

-   -   Miscellaneous\*\*\\

You can edit your *./.cdsint* or *./.cdsinit_local* and set your
preferred text editor as default as follows:

`editor = "/usr/bin/nedit"`

See also

<http://eda.engineering.wustl.edu/wiki/index.php/Cadence_Environment>\\
<https://secure.engr.oregonstate.edu/wiki/ams/index.php/Cadence/TipsAndTricks>

\\

-   -   License check out order\*\*\\

Use your local *.cdsenv* with

`license VSELicenseCheckOutOrder string "XL,L" license VLSLicenseCheckOutOrder string "GXL,XL,L" license ADELicenseCheckOutOrder string "GXL,XL,L"`

See also

<http://www.cadence.com/Community/forums/p/15176/26989.aspx> \\
<http://support.cadence.com/wps/mypoc/cos?uri=deeplinkmin:ViewSolution;solutionNumber=11587412>
(Cadence On-line support login required)

###### 
