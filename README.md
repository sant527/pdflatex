# HOW TO CHANGE PAGE SIZE IN THE MID OF THE DOCUMENT

## METHOD 1 (The following works in PDFLaTeX:)
https://tex.stackexchange.com/a/6838/221200

```latex
\documentclass[parskip=full]{scrartcl}
% this is required for pagenumber and also KOMAoptions to work
\usepackage[automark,headsepline,footsepline]{scrlayer-scrpage}
% the above both are required to show page number 
\usepackage{graphicx}
% the above package is required for includegraphics to work

\usepackage
  [showframe]% to show the page layout
  {geometry}

\begin{document}

\eject \pdfpagewidth=2.5in \pdfpageheight=6.0in
%The above changes the page size but its not sufficient because the margins are not change.
% So using newgeometry we have to readjust the margins and header and footer
\newgeometry{layoutwidth = 2.5in,layoutheight = 6.0in,left=0mm,right=0mm,top=0mm,bottom=0mm,footskip=1mm}
\includegraphics[width=\textwidth,keepaspectratio,page=6]{test123.pdf}
\includegraphics[width=\textwidth,keepaspectratio,page=6]{test123.pdf}
\includegraphics[width=\textwidth,keepaspectratio,page=6]{test123.pdf}

\eject \pdfpagewidth=6in \pdfpageheight=2.5in
\newgeometry{layoutwidth =6in,layoutheight = 2.5in,left=0mm,right=0mm,top=0mm,bottom=0mm,footskip=1mm}
LANDSCAPE

\end{document}
```

# METHOD 2 (using KOMA scripts)
https://tex.stackexchange.com/q/556939/221200

```latex
\documentclass[parskip=full]{scrartcl}
% this is required for pagenumber and also KOMAoptions to work
\usepackage[automark,headsepline,footsepline]{scrlayer-scrpage}
% the above both are required to show page number 
\usepackage{graphicx}
% the above package is required to includegraphics

\usepackage
  [showframe]% to show the page layout
  {geometry}

\begin{document}

\KOMAoptions{paper=2.5in:6.0in,DIV=calc}
\recalctypearea
% The above 2 commands change the page size, but still we have to adjust
% the margins using the below command
\newgeometry{layoutwidth = 2.5in,layoutheight = 6.0in,left=0mm,right=0mm,top=0mm,bottom=0mm,footskip=1mm}
\includegraphics[width=\textwidth,keepaspectratio,page=6]{test123.pdf}
\includegraphics[width=\textwidth,keepaspectratio,page=6]{test123.pdf}
\includegraphics[width=\textwidth,keepaspectratio,page=6]{test123.pdf}

\KOMAoptions{paper=6in:2.5in,DIV=calc,paper=landscape}
%NOTE:
% \KOMAoptions{paper=6in:2.5in,DIV=calc} will not work it will still show 2.5in x 6in
% as per documentation 
% Additionally, the size can also be specified either in the form width :height or in the form
% v3.22 height :width . Which value is taken as the height and which as the width depends on the
% orientation of the paper. With paper=landscape or paper=seascape, the smaller value is
% the height and the larger one is the width . With paper=portrait, the smaller value is the
% width and the larger one is the height .
% I THINK BY DEFAULT IS POTRAIT. So 2.5in x 6in will be shown
% if we want 6in x 2.5in then we have to explicitly mention paper=landscape

\recalctypearea
\newgeometry{layoutwidth =6in,layoutheight = 2.5in,left=0mm,right=0mm,top=0mm,bottom=0mm,footskip=1mm}
LANDSCAPE

\end{document}
```
