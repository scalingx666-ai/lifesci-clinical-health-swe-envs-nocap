# Build notes - Clinical & Health Informatics

Repo2RLEnv pr_diff (v0.9.6), Harbor-format output. Domain: clinical-health.

## Funnel

| Stage | Count |
|---|---|
| Domain candidates (deduped) | 523 |
| After active+star+noise filter | 271 |
| Final target list (cap unlimited) | 271 |
| Repos with >=1 task | 36 |
| Repos with 0 tasks | 214 |
| Total tasks (unlimited (no per-repo cap)) | 2959 |

## Generation

- Shared task bank: each repo generated once (pr_diff, limit=3,
  max_files_per_pr=15, min_loc_changed=2), 4-way concurrency,
  rate-limit-aware with .done checkpoint resume.
- Per-domain consolidation: rank by reward_calibration.loc_changed desc,
  keep ALL qualifying tasks (no per-repo cap). Zero-yield repos are NOT fabricated.
- Overlap with the 3 published cancer editions is allowed (user decision);
  domains are independent selections, not a partition of one repo set.

## Zero-yield repos (informational, 214)

- xinxuxin/keystone-bench
- MoH-Malaysia/covid19-public
- FirelyTeam/firely-net-sdk
- zou-group/sleepfm-clinical
- hms-dbmi/CHIEF
- informatici/openhospital
- xjtulyc/MedgeClaw
- re-search/DocProduct
- OpenClinica/OpenClinica
- microsoft/dicom-server
- ohcnetwork/care
- bluehalo/node-fhir-server-core
- MIT-LCP/eicu-code
- ehrbase/ehrbase
- obophenotype/human-phenotype-ontology
- LinuxForHealth/FHIR
- CogStack/OpenGPT
- healthylaife/MIMIC-IV-Data-Pipeline
- opensaludlab/ciencia_datos
- onblog/doctor
- OyadotAI/oya-browser
- masslight/ottehr
- fhirbase/fhirbase
- remotebiosensing/rppg
- cqframework/clinical_quality_language
- tuva-health/tuva-core
- bowang-lab/ecg-fm
- abachaa/Existing-Medical-QA-Datasets
- lucidrains/clinical-calculator-tooluse
- nHapiNET/nHapi
- LibreHealthIO/lh-ehr
- google/ground-android
- hgraph-os/hGraph
- openhealthcare/opal
- the-momentum/apple-health-mcp-server
- FirelyTeam/spark
- DIGI-UW/OpenELIS-Global-2
- sigven/pcgr
- NYUMedML/GNN_for_EHR
- epic-open-source/seismometer
- pharmaverse/teal
- heshanera/HealthPlus
- baichuan-inc/Baichuan-M3-235B
- iamarunbrahma/finetuned-qlora-falcon7b-medical
- analysiscenter/cardio
- StanfordSpezi/Spezi
- simpledotorg/simple-android
- judegomila/OnCo
- OpenIntegrationEngine/engine
- wardle/hermes
- som-shahlab/ehrshot-benchmark
- third-culture-software/bhima
- rexrodeo/american-healthcare-conundrum
- Genentech/BRAID
- healthchainai/HealthChain
- samply/blaze
- sammargolis/OpenScribe
- thetahealth/mirobody-env
- xliucs/MTTS-CAN
- beda-software/fhir-py
- WGLab/InterVar
- apple/FHIRModels
- ppazos/cabolabs-ehrserver
- hapifhir/org.hl7.fhir.core
- senaranya/HL7
- PharmGKB/PharmCAT
- LibertFan/AI_Hospital
- sepandhaghighi/nafas
- oehf/ipf
- McJackTang/MMPD_rPPG_dataset
- SciBlend/SciBlend
- cjyyx/ScreenFilter
- mlcommons/GaNDLF
- MAXNORM8650/MedAgentSim
- Vermonster/fhir-kit-client
- vanderschaarlab/autoprognosis
- HiLab-git/WORD
- Clinical-Genomics/scout
- cds-hooks/docs
- FredHutch/Oncoscape
- SiyuanYan1/PanDerm
- inferno-framework/fhir_client
- healthsites/healthsites
- healthymind-tech/Taiwan-Health-MCP
- bluehalo/graphql-fhir
- aphp/edsnlp
- bunnelab/virtues
- BCHSI/philter-ucsf
- MIT-LCP/mimic.mit.edu
- StanfordMIMI/clin-summ
- BiomedSciAI/fuse-med-ml
- Gurge44/EndlessHostRoles
- uf-hobi-informatics-lab/ClinicalTransformerNER
- htlin222/meta-pipe
- clips/clicr
- WeixiangYAN/ClinicalLab
- dcarbone/php-fhir
- muhammadusamakhan911-bit/fabric-mlv-agent-healthcare-starter
- ahmadfauzirahman99/simrs-api
- Project-Based-Learning-IT/healthcare-appointment-scheduling-app
- Project-MONAI/monai-deploy-app-sdk
- wshi83/EhrAgent
- apache/ctakes
- aehrc/pathling
- wso2/fhir-mcp-server
- shamil-t/ehr-blockchain
- syzygyhack/open-foundry
- youcc/healthcare_analytics_engineer_handbook
- jgc128/mednli
- deepmedicine/BEHRT
- uf-hobi-informatics-lab/ClinicalTransformerRelationExtraction
- Ahryman40k/typescript-fhir-types
- beda-software/fhir-emr
- BIMCV-CSUSP/BIMCV-COVID-19
- ruby-hl7/ruby-hl7
- nf-core/oncoanalyser
- nyuolab/NYUTron
- Project-MONAI/monai-deploy
- MIC-DKFZ/napari-nninteractive
- LHNCBC/lforms
- jeffshek/open
- HealthRex/CDSS
- starmpcc/Asclepius
- dentalpin/dentalpin
- DouglasNeuroInformatics/OpenDataCapture
- glee4810/EHRSQL
- Kalbra/NoReel
- VictorButoi/FleXray
- Doctor-One/doctor-dok
- MAGIC-AI4Med/DiagGym
- google/cql
- gematik/api-erp
- yashverma9/AI-Blockchain-Electronic-Health-Records-Management-System
- DosX-dev/SafeNova
- Ahus-AIM/Open-ECG-Digitizer
- rvandewater/YAIB
- ohs-foundation/fhir-gateway
- BerryWorksSoftware/edi-json
- samply/golang-fhir-models
- SaravananSubramanian/hl7
- cozygene/SLIViT
- pharmaverse/tern
- uwrit/leaf
- google/fhir-py
- SagaHealthcareIT/mirthsync
- albertzhzhou-droid/ParkinSUM
- som-shahlab/medalign
- baeseongsu/ehrxqa
- Efferent-Health/HL7-V2
- kdpsingh/clinspacy
- SafetyGraphics/safetyGraphics
- the-momentum/fhir-mcp-server
- MLD3/FIDDLE
- cyanheads/clinicaltrialsgov-mcp-server
- openmrs/openmrs-esm-patient-chart
- inferno-framework/fhir_models
- the-momentum/healthstack
- ZoliQua/React-Advanced-Odontogram
- openmrs/openmrs-module-fhir2
- starmpcc/CAMEL
- ivanwilliammd/satusehat-integration
- CMSgov/beneficiary-fhir-data
- HasteHealth/HasteHealth
- cqframework/cql-execution
- jmandel/health-skillz
- The-Swarm-Corporation/Open-MAI-Dx-Orchestrator
- RSNA/anonymizer
- shihjay2/nosh2
- CogStack/Foresight
- microsoft/azure-health-data-services-toolkit
- AdaptInfer/Contextualized
- beda-software/fhirpath-py
- yahskapar/personal-health-insights-agent
- Fan-Pier-Labs/openrecord
- pavanbadempet/AI-Healthcare-System
- FlixCoder/fhir-sdk
- LifeValue/HealthWallet.me
- YXNTU/EHRStruct
- wardle/hades
- HealthRex/PhysicianBench
- ohs-foundation/kotlin-fhir
- cqframework/cqf-ruler
- Mobile-Sensing-and-UbiComp-Laboratory/NormWear
- databricks-industry-solutions/smolder
- cqframework/CQL-Formatting-and-Usage-Wiki
- opensrp/fhircore
- instamed/healthcare-payments-blockchain
- Optum/CyFHIR
- microsoft/clinical-self-verification
- Outburn-IL/fume-community
- dermatologist/pyomop
- FerroHEALTH/FerroEHR
- MyLikita-Health/sudoEMR
- IMS94/chr247.com
- Kailona/ehr
- VectorInstitute/odyssey
- aehrc/smart-forms
- pramodramdas/digital_healthcare
- zzachw/llemr
- yhzhu99/HealthFlow
- CogStack/CogStack-NiFi
- ohs-foundation/fhir-app-examples
- smilecdr/FHIR.ts
- HeliosSoftware/hfs
- aphp/Cohort360-FrontEnd
- Okes2024/Early-Detection-of-Chronic-Diseases-from-EHRs
- edenlabllc/rmk
- som-shahlab/hf_ehr
- AIM-Harvard/SDoH
- bachlab/PsPM
- gematik/api-ti-messenger
- cqframework/clinical-reasoning
- dermatologist/fhiry
- justin13601/ACES

## Caveats

- Static validation only; real grading needs an LLM judge key + Docker.
- inline_dockerfile mode skips image build (no Docker daemon needed to publish).
- Provider secrets in upstream diffs were redacted before public release.
