## Sites com dicas do Virtuoso e/ou analógico

- https://miscircuitos.com/

## Dicas rápidas do site https://carleton.ca/doe/cadence-virtuoso-tips/:

* Lock files (cdslck):

  Cadence Virtuoso uses special files called lock files to designate designs that are currently open for edit. This is used to prevent a design from being edited from multiple users simultaneously. Unfortunately, if Virtuoso or your Linux session crashes, the lock files will still exist in your library directory and when you try to open the designs for edit, you will get an error. To fix this problem you have to delete the lock files.

* Adjust font size:

  Edit the .cdsinit to include the following

  hiSetFont(“label” ?size 18)
  
  hiSetFont(“text” ?size 18)

* Delta markers:

  You can easily add delta markers (markers that show the time or voltage difference between 2 points, possibly between different waveforms), by hovering the cursor over the first point and type “a”, then hover at the next point and type “b”.

  Alternatively, you can place 2 markers with the usual “m” key while hovering, then hold the Control key while clicking both markers to select both simultaneously, then type “Shift-d”.

* Changing ADE Default Load / Save Option to “Cellview”

  Default is “Directory” but saving states as cellviews is the preferred method (keeps everything organized by having your test bench schematic and simulation setup together); even Cadence recommends storing ADE states as cellviews and that the directory option is just for backward compatibility.
  
  To make “cellview” the default option when you go to load or save a state in ADE L, in the directory in which you run Virtuoso edit (or create) the .cdsinit file and somewhere (usually put all of your customizations at the end) add these lines (the first is just a comment reminding you what the next line does):
  
  ; make ADE L save / load state option default to cellview
  
  envSetVal("asimenv" "saveAsCellview" 'boolean t)
