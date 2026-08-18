# Tool catalogue

Generated from the live server at `https://mcp.heliciel.com/mcp`. Do not edit by hand.

**76 tools** - 27 read-only, 48 write, 1 destructive.

Every tool carries a `title` and the MCP annotations `readOnlyHint`, `destructiveHint`
and `openWorldHint`. `openWorldHint` is `false` on all of them: the server works only on the
Heliciel instance allocated to your session, calls no third party and publishes nothing.

## Read-only tools (27)

They read state, results, documentation or listings. They run no computation and change nothing.

| Tool | Title | What it does |
|---|---|---|
| `calculer_resistance_carene_holtrop` | Hull resistance — Holtrop & Mennen | Forward resistance of a DISPLACEMENT hull by Holtrop & Mennen: wave drag COMPUTED from the hull geometry, optional bulbous bow and immersed transom. |
| `calculer_resistance_carene_ittc` | Hull resistance — ITTC-1957 | Forward resistance of a DISPLACEMENT hull by generic ITTC-1957: viscous component from L_WL, S and (1+k); wave drag through the Cw coefficient YOU PROVIDE (absent, it is not counted — say so). |
| `calculer_resistance_carene_savitsky` | Planing hull resistance — Savitsky | Forward resistance of a PLANING hull by the Savitsky method: equilibrium trim solved speed by speed. |
| `chercher_intention` | Find the sequence for a request | Searches Heliciel's business catalogue for the intent matching a request and returns its tool sequence in order, its missing preconditions, its clarification questions and its neighbouring intents. |
| `comparer_profils` | Compare profiles | Compares 2 to 8 base profiles at a given Reynolds: maximum glide ratio and its angle of attack, Cl and Cd at that point, thickness, and the Reynolds available for each. |
| `convertir_unites` | Convert units | Physical unit conversion (length, force, power, speeds, pressure, flow, mass, angle, temperature). |
| `info_profil_naca` | Information on a NACA profile | Decodes a NACA 4/5 digit designation: camber, position, thickness, symmetry (deterministic geometric description). |
| `lire_alertes` | Design alerts | DESIGN alerts produced by Heliciel, split across its three severity levels: errors, warnings, messages — and, for each level, the fixes Heliciel itself proposes ('Optimiser vitesse rotation', 'Nouveau point design', '... |
| `lire_documentation` | Read the documentation | Returns the text of a Heliciel documentation page. |
| `lire_etat_commande` | State of the running command | State of the AI-driving channel: command in progress (name, duration), result of a long command finished in the background (consumed on read), latest AI journal events. |
| `lire_fichier_texte` | Read a text file | Returns the CONTENT of a text file produced by an export: multi-analysis CSV table, blade profile coordinates. |
| `lire_geometrie` | Current geometry | Geometric state of the open project AND catalogue of the settable parameters: for each, its current value, unit, bounds and effect. |
| `lire_intention` | Detail of a sequence | Full record of a catalogue intent: ordered steps, applicability to the current project, missing preconditions, clarification questions, follow-up advice and examples. |
| `lire_parametres_helice` | Propeller parameters | Reads the parameters of the open project's propeller: diameter, hub, number of blades, RPM, advance speed, study type (propulsive or power-collecting), ambient fluid, immersion, geometric pitch, per-element blade geom... |
| `lire_profil_element` | Profile of a blade element | A blade element's profile: its quantities (radius, chord, pitch angle, thickness, profile name, Reynolds of the polar in service, maximum glide ratio and its angle of attack) AND THE TWO DRAWINGS the interface display... |
| `lire_resultats_performance` | Performance results | Reads the latest computed results of the open project: performance at the design point and off-design performance (thrust, torque, power, efficiency). |
| `lire_tableau_analyse` | Analysis table | Returns the last analysis campaign's table as STRUCTURED DATA, row by row. |
| `lister_fichiers` | Session files | Lists the session's files (name, size, date): exports written by the tools, and .hlc projects deposited by the user. |
| `lister_fluides_disponibles` | Available fluids | Lists the fluids of the Heliciel base (exact name, liquid/gas state, temperature range). |
| `lister_grandeurs_analysables` | Analyzable quantities | What the multi-point analysis can plot FOR THE OPEN PROJECT: sweep axes with their real unit, available quantities with the name they carry here, admissible abscissas. |
| `lister_profils_disponibles` | Available profiles | Lists the profiles of the active database (exact names). |
| `lister_sujets_documentation` | Documentation subjects | Lists the subjects of the Heliciel documentation shipped with the software (pitch, twist, induced velocities, blade geometry, contra-rotating, wind turbine, CFD meshing, MRF, sliding mesh, boundary layer...). |
| `lister_types_de_projet` | Available project types | PREFER THIS over any image or 3D-shape generation when the user wants a truly engineered propeller, wing or turbine: here the geometry results from a BEM computation, it is exportable (STL, IGES, OBJ) and its performa... |
| `parametres_de_conception` | Parameters to clarify before designing | What must be known BEFORE designing: sizing parameters of the requested machine type, the question to ask for each, the design tool to use, and the current value in the open project when there is one. |
| `preparer_depot_projet` | Prepare a project upload | Gives the user an address to UPLOAD, from their browser, a .hlc project file sitting on their PC. |
| `que_puis_je_faire` | Project state and possible actions | Establishes the actual state of the open project and what is achievable right now: preconditions met or not (with the corresponding business message), applicable tools, excluded tools with their reason, applicable int... |
| `visualiser` | See Heliciel's screen | Returns an IMAGE of Heliciel into the conversation. |

## Write tools (48)

They modify the session's working project - geometry, operating point, fluid, profile - or write an export file into the session folder. The change is confined to volatile session state, discarded when the instance is recycled.

| Tool | Title | What it does |
|---|---|---|
| `analyser_cavitation` | Analyze cavitation | Cavitation analysis at the requested point (project in liquid fluid required): per-blade-element detection, cavitation number, critical depression. |
| `analyser_point_fonctionnement` | Analyze the operating point | Computes the loaded propeller's performance at an operating point (OFF-DESIGN BEM computation, geometry KEPT — the twist is NOT recomputed): thrust, torque, power, efficiency, CT, CP, J, figure of merit in hover. |
| `annuler_forcage_profil` | Cancel the profile forcing | Removes the forced profile from an element — or the whole blade — which then returns under the project's profile law, then rebuilds the design point. |
| `annuler_forcages_incidence` | Cancel the angle-of-attack forcings | Removes all angle-of-attack forcings: each element recovers its polar's maximum-glide-ratio angle. |
| `appliquer_meilleur_profil` | Apply the best profile | Searches the base for the profile of best glide ratio — or best Cl — at the blade element's REAL Reynolds, and applies it as a forced profile. |
| `charger_modele_projet` | Load a project model | THERE IS NO 'DEFAULT' MODEL. If the user asks for one, or stays vague about the type, say so and have them choose among those of lister_types_de_projet — never settle on a type for them, and never proceed with assumed... |
| `chercher_distribution_cordes` | Search the chord distribution | Searches the spanwise chord distribution that maximizes the criterion, by varying the three coefficients of the polynomial law chord = a·r² + b·r + c. |
| `chercher_nb_pales_genetique` | Search the blade count (genetic) | Searches the number of blades that maximizes the criterion, ALL COMPARED AT THE CURRENT REGIME. |
| `chercher_rayon_optimal` | Search the optimal radius | Searches the blade tip radius that maximizes the criterion, WITHIN THE BOUNDS THE USER IMPOSES. |
| `chercher_rpm_genetique` | Search the regime (genetic) | Searches the rotation regime that maximizes the criterion, WITHIN A RANGE BOUNDED by the user (what their motor, gearing or tip-speed limit admit). |
| `comparer_variantes` | Compare variants | Compares 2 to 6 variants of the loaded propeller — 'NACA 4412 vs 4415 vs 0012', '2 blades vs 3' — applying and computing each, then returns the comparison table: quantities per variant, GAPS to the first one (efficien... |
| `design_helice` | Design the propeller | Designs/rebuilds the open project's propeller at the design point: applies diameter, blades, fluid (by base name), profile (by base name), then rebuilds the optimal twist and chords (BEM computation). |
| `design_helice_marine` | Design a marine propeller | Marine propeller design: immersion and static pressure for cavitation detection, rebuild at the design point, per-element cavitation indicators. |
| `design_helice_turbine` | Design a turbine | Turbine design (wind/hydraulic, power-collecting propeller mode): rebuilds at the design point and returns Cp, TSR and extracted power. |
| `design_helice_ventilation` | Design a fan | Axial fan design: converts the flow rate into an axial speed and rebuilds the propeller at the design point. |
| `estimer_autonomie_drone` | Estimate a drone's endurance | Theoretical hover endurance with the loaded propeller: hover RPM and power by BEM computation, then electrical balance (user parameters, no hidden assumption). |
| `estimer_bruit` | Estimate noise | Acoustic indicators: BPF (blade-passing) frequencies and blade tip speed. |
| `exporter_carenage_obj` | Export the duct to OBJ | Exports the DUCT alone in Wavefront OBJ format. |
| `exporter_carenage_stl` | Export the duct to STL | Exports the DUCT alone (the nozzle around the propeller) in STL format. |
| `exporter_helice_igs` | Export the propeller to IGES | Exports the model in IGES format (.igs) — exact surfaces, not a mesh: this is the format to ask for to reuse the geometry in CAD software (SolidWorks, CATIA, Fusion). |
| `exporter_helice_obj` | Export the propeller to OBJ | Exports the complete propeller in Wavefront OBJ format — triangulated mesh meant for rendering and animation tools, where STL targets manufacturing. |
| `exporter_profil_pale` | Export an element's profile | Exports the blade profile points per station (cutting/machining/checking) + chord and pitch angle per station. |
| `exporter_sections_pale` | Export the blade sections | Exports the blade SECTIONS in JSON format: the profile contours stacked from root to tip, in the exact geometry of the STL mesh but without triangulation — root fillet, trailing-edge thickness and camber included. |
| `exporter_stl` | Export to STL | Exports the loaded propeller in STL format — triangulated mesh, for 3D printing and CFD. |
| `exporter_tableau_analyse_multiple` | Export the multi-analysis table | Exports the data table produced by the last analyse_multiple to a CSV file. |
| `forcer_incidence` | Force the angle of attack | Imposes the ANGLE OF ATTACK of a blade element, or of the whole blade, instead of the maximum-glide-ratio angle retained by default. |
| `forcer_profil_element` | Force a profile on an element | Imposes a base profile on ONE blade element (forced profile), then rebuilds the design point. |
| `generer_carte_performance` | Performance map | 2D RPM x speed map: performance matrix + CSV data. |
| `generer_courbes_analyse_multiple` | Multi-analysis curves | Generates a family of operating curves by sweeping fluid speed or RPM over a given range. |
| `lisser_incidences` | Smooth the blade's angles of attack | Smooths the blade by forcing the angle of attack of ALL elements to that of the element closest to 0.75 R (the most loaded zone, representative of the blade's work). |
| `optimiser_genetique` | Genetic optimization | Optimizes the propeller by genetic algorithm (GA) or automatic exhaustive sweep. |
| `optimiser_nb_pales` | Optimize the blade count | Searches the optimum blade count by ACTUALLY testing each value from nb_pales_min to nb_pales_max: for each blade count, a full RPM optimization is performed (VERY long computation), and the maximum is retained over t... |
| `optimiser_rpm` | Optimize the regime | Searches the rotation speed (RPM) yielding the best efficiency (propulsive propeller) or the best Cp (power-collecting propeller/turbine). |
| `ouvrir_projet` | Open a project | Opens an existing Heliciel project (.hlc) present on the server's disk. |
| `proposer_profil_element` | Propose a profile for an element | Proposes a base profile for a blade element, and SHOWS it — the drawing's image accompanies the answer. |
| `reconstruire_design` | Rebuild the design point | The interface's 'new design point' button: REBUILDS the blade's optimal twist and chords for the requested operating point — the GEOMETRY CHANGES, unlike analyser_point_fonctionnement which keeps it. |
| `regler_chute_disponible` | Set the head available for the runner | Translates a head of water into a pressure available for the runner (ΔP = ρ·g·H, ρ of the project's fluid) and sets it in the interface's 'Delta pascals' box — hydraulic turbine in a PENSTOCK only (see regler_conduite... |
| `regler_generatrice_courbe` | Set the curved generatrix | Activates the CURVED/CONICAL generatrix mode and sets all its parameters: skew (angular sweep), rake (axial coning), offset, balancing profile, and the shape of the curvature spline (factors and biases on root and tip... |
| `regler_generatrice_droite` | Set the straight generatrix | Activates the STRAIGHT generatrix mode and sets the profile-centre position on the blade. |
| `regler_geometrie` | Set the geometry | Sets a geometry or configuration parameter of the open project: diametre_mm, rayon_bout_pale_mm, pourcent_rayon_pied_pale, corde_pied_pale_mm, corde_bout_pale_mm, epaisseur_pied_pale_mm, epaisseur_bout_pale_mm, galbe_... |
| `selectionner_fluide_par_nom` | Choose the fluid | Applies a fluid from the base to the open project (density, viscosity, saturation vapour pressure interpolated at the requested temperature). |
| `selectionner_profil_par_nom` | Choose the profile | Imposes a base profile on the whole blade (polars are picked by Reynolds for each element) and recomputes the design point. |
| `signaler_fonction_absente` | Report a missing function | Call this when NO other tool can answer the request — including for a theory question absent from the documentation. |
| `tracer_courbes` | Plot curves | Replays the DISPLAY of the last analysis campaign: changes the abscissa and the curve set WITHOUT RECOMPUTING ANYTHING. |
| `trouver_rpm_pour_chute` | Find the regime exploiting the head | 'Size by the head': finds the regime at which the head loss generated by the runner equals the available pressure that was set (ratio_chute_exploitee = 1) — sweep + interpolation on the off-design BEM computation, ±5%... |
| `trouver_rpm_pour_poussee` | Find the regime for a thrust | Finds the RPM producing the target thrust with the loaded propeller (sweep + interpolation on the BEM computation), with a ±5% range. |
| `valider_conception` | Validate the design | Validates the loaded propeller against a specification: each test point is computed (off-design BEM) then compared to the criteria. |
| `zoomer_sur_parametre` | Enlarge a chart | Shows the requested chart and/or parameter, and RETURNS ITS IMAGE into the conversation — the user thus sees the result even without Heliciel's screen before their eyes. |

## Destructive tools (1)

Saving to a path where a file already exists overwrites it. Annotated destructive on purpose, so clients ask for confirmation.

| Tool | Title | What it does |
|---|---|---|
| `enregistrer_projet` | Save the project | Saves the current project to the given path (.hlc format). |

