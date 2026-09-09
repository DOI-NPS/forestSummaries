# forestSummaries
This repo contains scripts and R markdown reports that generate park-level automated summaries as paged html files of MIDN, NCBN, and NETN 
forest data and compiles the shapefiles used in the map based summaries that are constructed in ArcGIS Pro.

Notes on this repo:
<ul>
<li>Mid-Atlantic and Northeast Coastal and Barrier Network parks are checked using scripts starting with "MIDN".</li>
<li>Northeast Temperate Network parks are checked using scripts starting with "NETN".</li>
<li>ACAD and SAHI have their own reports because ACAD has so many plots, and SAHI sites are all sampled within the same year. </li> 
<li>For each network, their corresponding R package must be installed and either access to the SQL server or exported views as CSVs 
must be imported. To install the forestNETN package, run `pak::pkg_install('doi-nps/forestNETN')`. For the MIDN/NCBN forest package, 
run `pak::pkg_install('doi-nps/forestMIDN')`</li>
<li>Previous archived versions of this repo can be found at <a href="www.github.com/katemmiller/forestSummaries">
www.github.com/katemmiller/forestSummaries</a></li>
</ul>

This package includes the following reports and their dependencies in the order they run: 
<ul>
<li><b>ACAD_figures_and_tables.Rmd:</b> paged html report for ACAD-only. Given there are so many more plots than other parks, 
it was easier to build this rmd separately. Note, however that only 2 ACAD-specific scripts are sourced (see below).</li>
  <ul>
  <li>source_script_ACAD.R: sets up output folders and params used in remaining scripts.</li>
  <li>scripts/forest_summary_code_ACAD.R: generates shapefiles for ArcGIS maps and Figure 3 and all Tables. </li>
  <li>scripts/regen_debt_metrics_NETN.R: calculates metrics for regeneration debt and creates Figs 1 and 2.</li>
  <li>scripts/tree_regen_stem_changes_by_species_loess_NETN.R: generates Figs 4 - 6.</li>
  </ul>
<li><b>ASIS_figures_and_tables.Rmd:</b> paged html report for ASIS-only. This report was only needed for ASIS when there was
only one cycle of data. Now that repeated visits are occurring, this is more of a template in case new parks are ever added.</li>
  <ul>
  <li>source_script_ASIS.R: sets up output folders and params used in remaining scripts.</li>
  <li>scripts/forest_summary_code_ASIS.R: generates shapefiles for ArcGIS maps and Figure 3 and all Tables. </li>
  <li>scripts/regen_debt_metrics_ASIS.R: calculates metrics for regeneration debt and creates Figs 1 and 2.</li>
  <li>scripts/tree_regen_stem_changes_by_species_loess_ASIS.R: generates Figs 4 - 6.</li>
  </ul>
<li><b>MIDN_figures_and_tables.Rmd:</b> paged html report for all MIDN and NCBN parks besides SAHI.</li>
  <ul>
  <li>source_script_MIDN.R: sets up output folders and params used in remaining scripts.</li>
  <li>scripts/forest_summary_code_MIDN.R: generates shapefiles for ArcGIS maps and Figure 3 and all Tables. </li>
  <li>scripts/regen_debt_metrics_MIDN.R: calculates metrics for regeneration debt and creates Figs 1 and 2.</li>
  <li>scripts/tree_regen_stem_changes_by_species_loess_MIDN.R: generates Figs 4 - 6.</li>
  </ul>
<li><b>NETN_figures_and_tables.Rmd:</b> paged html report for all NETN parks except ACAD.</li>
  <ul>
  <li>source_script_NETN.R: sets up output folders and params used in remaining scripts.</li>
  <li>scripts/forest_summary_code_NETN.R: generates shapefiles for ArcGIS maps and Figure 3 and all Tables. </li>
  <li>scripts/regen_debt_metrics_NETN.R: calculates metrics for regeneration debt and creates Figs 1 and 2.</li>
  <li>scripts/tree_regen_stem_changes_by_species_loess_NETN.R: generates Figs 4 - 6.</li>
  </ul>
  
<li><b>/scripts/supplemental_subunit_figures_MIDN.Rmd:</b> paged html report for an individual subunit in a given
MIDN park.</li>
<li><b>/scripts/supplemental_subunit_figures_NETN.Rmd:</b> paged html report for an individual subunit in a given
NETN park.</li>
<li><b>ACAD_tree_growth_figures.Rmd:</b> tabbed report looking at tree growth and mortality of individual plots and 
species in ACAD to examine potential </li>
<li><b>ACAD_tree_growth_figures_abbrev.Rmd:</b> same tabbed report as above but without individual plots to keep report small enough
for email.</li>
</ul>

Helper scripts to iterate generating reports for multiple parks, plots, etc:
<ul>
<li>MIDN_figures_and_tables_pdf: Automates generating paged html reports for list of MIDN parks, and converting the paged 
html documents into pdfs.</li>
<li>NETN_figures_and_tables_pdf: Automates generating paged html reports for list of NETN parks, and converting the paged 
html documents into pdfs.</li>
</ul>

Important files to help with parameter set up:
<ul>
<li>MIDN_NCBN_indicator_species.csv: history of indicator species list used to filter on original indicator list.</li>
<li>MIDN_MetaData.csv: contains park long names.</li>
<li>MIDN_MetaData_Subunits.csv: contains subunit long names.</li>
<li>MIDN_params.csv: shows the start and end year for all monitoring, the start and end year for the current 4-year cycle,
and the current cycle number. <b>UPDATED EVERY YEAR.</b></li>
<li>NETN_MetaData.csv: contains park long names.</li>
<li>NETN_MetaData_Subunits.csv: contains subunit long names.</li>
<li>NETN_params.csv: shows the start and end year for all monitoring, the start and end year for the current 4-year cycle,
and the current cycle number. <b>UPDATED EVERY YEAR.</b></li>
<li>NPS_tree_species_groups.csv: species groups to help simplify maps (note these are just a starting point).</li>
<li>tree_conditions_table.csv: spells out long names of tree condition abbreviations.</li>
<li>scripts/VT_RTE_Species.csv: Downloaded from VT Natural Heritage Program website to identify any rare, threatened, or endangered
species detected during monitoring in MABI.</li>
</ul>

<b>Note: Because file paths are not allowed through DGEC, there are places within these reports that require paths 
to be updated. If you try to knit a report, and you get an error about a file path not found, track down where the 
error occurred, and update the path to your computer. Be sure not to then push that path to DOI-NPS.</b> 

<b>Note 2: Several reports connect to a server using a CSV with the SQL server address that is not posted to GitHub, 
and lives in a file at the same level as the repo folder. Kate Miller can send that CSV to folks with access to the 
SQL server.</b>

