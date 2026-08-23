# Dataset

## Dataset Used

The fine-tuning experiment used an Indian legal Question-Answer dataset covering provisions of India's new criminal laws:

- Bharatiya Nyaya Sanhita (BNS), 2023
- Bharatiya Nagarik Suraksha Sanhita (BNSS), 2023
- Bharatiya Sakshya Adhiniyam (BSA), 2023

The dataset was obtained from the Hugging Face dataset:

`GSMS-B/Indian-Legal-QA-BNS-BNSS-BSA`

## Dataset Size

After resolving the dataset schema issue and selecting the required fields, the training dataset contained:

**6,354 examples**

## Dataset Fields

The processed dataset contains the following fields:

| Field | Description |
|---|---|
| `chunk_id` | Identifier for the legal content |
| `act` | Name of the relevant Act |
| `section_number` | Relevant legal section |
| `section_title` | Title of the section |
| `question` | Legal question |
| `answer` | Corresponding legal answer |
| `question_type` | Type/category of the question |

## Example

### Question

> Who is liable for punishment under the Indian criminal code for offences committed outside India?

### Answer

> Any person liable under Indian law to be tried for an offence committed beyond India will be dealt with as if the act was committed within India.

The answer also contains a reference to the relevant legal provision.

## Data Preparation

The original dataset was converted into an instruction-based format suitable for supervised fine-tuning.

The model was trained using an Alpaca-style prompt structure:

```text
### Instruction:
{}

### Input:
{}

### Response:
{}
