---
title: "Data Protection and Anonymization"
date: 2022-07-31T09:14:01+03:00
draft: true
tags: ["presidio", "data", "privacy"]
author: "Omer Segev"
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: ""
disableHLJS: false
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
---

Mining health data can lead to faster medical decisions, improvement in the quality of treatment, disease prevention, reduced cost, and it drives innovative solutions within the healthcare sector.  
However, health data is highly sensitive and subject to regulations such as the General Data Protection Regulation (GDPR), which aims to ensure patient's privacy.  
Anonymization or removal of patient identifiable information, though the most conventional way, is the first important step to adhere to the regulations and incorporate privacy concerns.   

In this post, I'll review a Python package created my Microsoft that helps to ensure sensitive data is properly managed and governed.  
It provides fast identification and anonymization modules for private entities in text and images such as credit card numbers, names, locations, social security numbers, bitcoin wallets, US phone numbers, financial data and more..  
 

* Allow organizations to preserve privacy in a simpler way by democratizing de-identification technologies and introducing transparency in decisions.
* Embrace extensibility and customizability to a specific business need.
* Facilitate both fully automated and semi-automated PII de-identification flows on multiple platforms.

## Install
```bash
pip install presidio-analyzer
pip install presidio-anonymizer
python -m spacy download en_core_web_lg
```
## Sample Code

```python
from presidio_analyzer import AnalyzerEngine
from presidio_anonymizer import AnonymizerEngine

text="""
PATIENT: JOHN SMITH
DOB: 5/5/1955
FILE #: 12345
PHYSICIAN: REFERRING
EXAM: MRI ABDOMEN WITH CONTRAST
DATE: 1/1/2011

Evaluation of the neck reveals a somewhat heterogeneous but well defined lobulated mass within the superficial
lobe of the anterior right parotid gland. The mass demonstrates a rounded focus of signal prolongation with
enhancement. The mass measures approximately 0.8 x 0.9 x 0.7 CM (anterior-posterior by transverse by superiorinferior). This appears similar to that noted on the prior CT. The mass just abuts the retromandibular vein, patent and medial to the right parotid duct. The mass is most consistent with a benign pleomorphic adenoma. No leftsided parotid mass is seen. Right and left submandibular glands are unremarkable.
The mucosal surfaces of the upper aerodigestive tract appear symmetric and unremarkable. The larynx is intact.
The nasopharynx is symmetric without distinct lesion.
The tongue and tongue base appear symmetric and unremarkable. The median raphe is midline.
The thyroid gland appears symmetric without distinct nodule.
No pathologically enlarged lymph nodes are found. The visualized lymph nodes demonstrate no central necrosis
or extranodal extension.
The right and left faucial tonsil is symmetric and unremarkable. The lingual tonsillar tissue appears symmetric
and of normal volume. The posterior nasopharyngeal lymphoid tissue does not appear enlarged.
Evaluation of the paranasal sinuses reveals no significant sinus inflammatory disease. No air-fluid levels are
noted.
The central skull base is intact. The central petrous temporal bones and mastoids remain clear. The visualized
base of brain appears unremarkable.
Cervical spondylosis is noted, most notable for a broad-based disc bulge and dorsal osteophytic ridge at the C5/6
level with a C6/7 level focal 2 mm central disc protrusion and dorsal osteophytic ridging, resulting in mild central
spinal stenosis. Mild foraminal narrowing also evident bilaterally.
"""

# Set up the engine, loads the NLP module (spaCy model by default) 
# and other PII recognizers
analyzer = AnalyzerEngine()

# Call analyzer to get results
results = analyzer.analyze(text=text,language='en')
print(results)

# Analyzer results are passed to the AnonymizerEngine for anonymization

anonymizer = AnonymizerEngine()

anonymized_text = anonymizer.anonymize(text=text,analyzer_results=results)

print(anonymized_text)
```

### The output
```
text:
PATIENT: <PERSON>: <DATE_TIME>
FILE #: 12345
PHYSICIAN: REFERRING
EXAM: MRI ABDOMEN WITH CONTRAST
DATE: <DATE_TIME>

Marked hydronephrosis and hydroureter are present in the right kidney (series 12 images <DATE_TIME>). Low signal
intensity foci in the proximal right ureter (series 6 image 36) likely represents flow related artifact. Possible
septations may be present in the distal right ureter (series 12 image 20). CT scan of the abdomen and pelvis with
and without contrast is recommended to evaluate for possible stone or distal obstructing lesion. Findings are new
since the previous examination. Decreased enhancement of the right kidney in comparison to the left during the arterial phase (series 15 image 35) may reflect a renal compromise. Stable mild <PERSON> is again noted in the
left kidney. No mass is identified in the kidneys. No masses seen along the right ureter. Postoperative changes are
seen from a distal pancreatectomy and cholecystectomy representing previous <PERSON> procedure. There is
dilatation of the pancreatic duct in the body and tail (series 6 images 23-20). No recurrent mass is
seen in the pancreas or anastomosis.
There is mild prominence of the biliary ducts in the left hepatic lobe (series 7 image 20). No filling defect is seen
within the common duct. <PERSON> and adrenal glands are unremarkable. No free fluid or lymphadenopathy seen.
No bowel obstruction is identified. Anterior abdominal hernia is again noted containing small bowel without
evidence of strangulation (series 7 image 33).
There is marked S-shaped scoliosis of the thoracolumbar spine. No metastatic bone lesions are identified.

items:
[
    {'start': 1296, 'end': 1304, 'entity_type': 'PERSON', 'text': '<PERSON>', 'operator': 'replace'},
    {'start': 987, 'end': 995, 'entity_type': 'PERSON', 'text': '<PERSON>', 'operator': 'replace'},
    {'start': 764, 'end': 772, 'entity_type': 'PERSON', 'text': '<PERSON>', 'operator': 'replace'},
    {'start': 206, 'end': 217, 'entity_type': 'DATE_TIME', 'text': '<DATE_TIME>', 'operator': 'replace'},
    {'start': 105, 'end': 116, 'entity_type': 'DATE_TIME', 'text': '<DATE_TIME>', 'operator': 'replace'},
    {'start': 20, 'end': 31, 'entity_type': 'DATE_TIME', 'text': '<DATE_TIME>', 'operator': 'replace'},
    {'start': 10, 'end': 18, 'entity_type': 'PERSON', 'text': '<PERSON>', 'operator': 'replace'}
]

```