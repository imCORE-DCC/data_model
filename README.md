# imCORE Data Model

Versioned history of the imCORE data model.

## Setup

These instructions assumes that you have Python 3 (with pip) and Git installed.

```console
# Clone data model repository
git clone https://github.com/imCORE-DCC/data_model.git imcore_data_model
cd imcore_data_model

# Install dependencies
python3 -m venv venv/
source venv/bin/activate
python3 -m pip install git+https://github.com/Sage-Bionetworks/schematic@bgrande/imcore

# Initialize schematic
schematic init --config ./config.yml
```

## CSV to JSON-LD Conversion

These instructions assume that you're in the repository and have already installed the dependencies using the above instructions.

```console
# Activate virtual environment with dependencies
source venv/bin/activate

# Use schematic to convert CSV data model to JSON-LD
schematic schema convert --base_schema ./minimal.model.jsonld ./imcore.model.csv
```

## Manifest Generation

These instructions assume that you're in the repository and have already installed the dependencies and generated the JSON-LD data model using the above instructions. The `<component>` placeholder should be replaced with the component label (_i.e._ the version without spaces or special characters). Here, this could be `BulkRNAseqLevel1`, `CyTOFBatchLevel`, or `Biospecimen`. The `<synapse_id>` placeholder should be replaced with the Synapse ID of a Synapse dataset folder that already contains the data files to be annotated.

```console
# Activate virtual environment with dependencies
source venv/bin/activate

# Use schematic to generate an empty manifest template
schematic manifest --config ./config.yml get --sheet_url --oauth --data_type <component>

# OR 

# Use schematic to generate a manifest template for a given Synapse dataset
schematic manifest --config ./config.yml get --sheet_url --oauth --data_type <component> --dataset_id <synapse_id>
```
