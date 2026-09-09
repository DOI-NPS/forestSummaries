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
<li><u>ACAD_figures_and_tables.Rmd:</u> paged html report for ACAD-only. Given there are so many more plots than other parks, 
it was easier to build this rmd separately. Note, however that only 2 ACAD-specific scripts are sourced (see below).</li>
  <ul>
  <li><u>source_script_ACAD.R:</u> sets up output folders and params used in remaining scripts.</li>
  <li><u>scripts/forest_summary_code_ACAD.R:</u> generates shapefiles for ArcGIS maps and Figure 3 and all Tables. </li>
  <li><u>scripts/regen_debt_metrics_NETN.R:</u> calculates metrics for regeneration debt and creates Figs 1 and 2.</li>
  <li><u>scripts/tree_regen_stem_changes_by_species_loess_NETN.R:</u> generates Figs 4 - 6.</li>
  </ul>
<li><u>ASIS_figures_and_tables.Rmd:</u> paged html report for ASIS-only. This report was only needed for ASIS when there was
only one cycle of data. Now that repeated visits are occurring, this is more of a template in case new parks are ever added.</li>
  <ul>
  <li><u>source_script_ASIS.R:</u> sets up output folders and params used in remaining scripts.</li>
  <li><u>scripts/forest_summary_code_ASIS.R:</u> generates shapefiles for ArcGIS maps and Figure 3 and all Tables. </li>
  <li><u>scripts/regen_debt_metrics_ASIS.R:</u> calculates metrics for regeneration debt and creates Figs 1 and 2.</li>
  <li><u>scripts/tree_regen_stem_changes_by_species_loess_ASIS.R:</u> generates Figs 4 - 6.</li>
  </ul>
<li><u>MIDN_figures_and_tables.Rmd:</u> paged html report for all MIDN and NCBN parks besides SAHI.</li>
  <ul>
  <li><u>source_script_MIDN.R:</u> sets up output folders and params used in remaining scripts.</li>
  <li><u>scripts/forest_summary_code_MIDN.R:</u> generates shapefiles for ArcGIS maps and Figure 3 and all Tables. </li>
  <li><u>scripts/regen_debt_metrics_MIDN.R:</u> calculates metrics for regeneration debt and creates Figs 1 and 2.</li>
  <li><u>scripts/tree_regen_stem_changes_by_species_loess_MIDN.R:</u> generates Figs 4 - 6.</li>
  </ul>
<li><u>NETN_figures_and_tables.Rmd:</u> paged html report for all NETN parks except ACAD.</li>
  <ul>
  <li><u>source_script_NETN.R:</u> sets up output folders and params used in remaining scripts.</li>
  <li><u>scripts/forest_summary_code_NETN.R:</u> generates shapefiles for ArcGIS maps and Figure 3 and all Tables. </li>
  <li><u>scripts/regen_debt_metrics_NETN.R:</u> calculates metrics for regeneration debt and creates Figs 1 and 2.</li>
  <li><u>scripts/tree_regen_stem_changes_by_species_loess_NETN.R:</u> generates Figs 4 - 6.</li>
  </ul>
  
<li><u>/scripts/supplemental_subunit_figures_MIDN.Rmd:</u> paged html report for an individual subunit in a given
MIDN park.</li>
<li><u>/scripts/supplemental_subunit_figures_NETN.Rmd:</u> paged html report for an individual subunit in a given
NETN park.</li>
<li><u>ACAD_tree_growth_figures.Rmd:</u> tabbed report looking at tree growth and mortality of individual plots and 
species in ACAD to examine potential </li>
<li><u>ACAD_tree_growth_figures_abbrev.Rmd:</u> same tabbed report as above but without individual plots to keep report small enough
for email.</li>
</ul>

Helper scripts to iterate generating reports for multiple parks, plots, etc:
<ul>
<li><u>MIDN_figures_and_tables_pdf.R:</u> Automates generating paged html reports for list of MIDN parks, and converting the paged 
html documents into pdfs.</li>
<li><u>NETN_figures_and_tables_pdf.R:</u> Automates generating paged html reports for list of NETN parks, and converting the paged 
html documents into pdfs.</li>
</ul>

Important files to help with parameter set up:
<ul>
<li><u>MIDN_NCBN_indicator_species.csv:</u> history of indicator species list used to filter on original indicator list.</li>
<li><u>MIDN_MetaData.csv:</u> contains park long names.</li>
<li><u>MIDN_MetaData_Subunits.csv:</u> contains subunit long names.</li>
<li><u>MIDN_params.csv:</u> shows the start and end year for all monitoring, the start and end year for the current 4-year cycle,
and the current cycle number. <u>UPDATED EVERY YEAR.</u></li>
<li><u>NETN_MetaData.csv:</u> contains park long names.</li>
<li><u>NETN_MetaData_Subunits.csv:</u> contains subunit long names.</li>
<li><u>NETN_params.csv:</u> shows the start and end year for all monitoring, the start and end year for the current 4-year cycle,
and the current cycle number. <u>UPDATED EVERY YEAR.</u></li>
<li><u>NPS_tree_species_groups.csv:</u> species groups to help simplify maps (note these are just a starting point).</li>
<li><u>tree_conditions_table.csv:</u> spells out long names of tree condition abbreviations.</li>
<li><u>scripts/VT_RTE_Species.csv:</u> Downloaded from VT Natural Heritage Program website to identify any rare, threatened, or endangered
species detected during monitoring in MABI.</li>
</ul>

<u>Note: Because file paths are not allowed through DGEC, there are places within these reports that require paths 
to be updated. If you try to knit a report, and you get an error about a file path not found, track down where the 
error occurred, and update the path to your computer. Be sure not to then push that path to DOI-NPS.</u> 

<u>Note 2: Several reports connect to a server using a CSV with the SQL server address that is not posted to GitHub, 
and lives in a file at the same level as the repo folder. Kate Miller can send that CSV to folks with access to the 
SQL server.</u>

