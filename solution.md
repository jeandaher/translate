## Transaction Table    

Transco 

| Code     |      Name     |  StatusLabel |  StatusMessage |
|----------|:--------------|:-------------|:---------------|
| TRS1     | Trans 1       | Initial      | Step           |


### Methods:     
1. APEX Label by language    
2. APEX Using Custom Label
3. Manage Multi language in LWC **(COMPLEX TO AVOID)**: create one component for all label, import it in the component, manage table by state, etc     


### Method 1. APEX Label by language     
| Code     |      Name     |  StatusLabel |StatusLabel_fr  |  StatusLabel_it   |  StatusMessage    |  StatusMessage_fr |  StatusMessage_it |
|----------|:------------- |:-------------|:---------------|:------------------|:------------------|:------------------|:------------------|
| TRS1     | Trans 1       | Initial      | Initiale       |Iniziale           | Step              | Etape             | Fare un passo     |


### Method 2. APEX Using Custom Label
same structure    
| Code     |      Name     |  StatusLabel |  StatusMessage |
|----------|:--------------|:-------------|:---------------|
| TRS1     | Trans 1       | Initial      | Step           |


### Create 2 Custom Labels :    
TRANS_STATUS_LABEL    
TRANS_STATUS_MESSAGE    

### Use Case, adding Spanish Language !    

The procedure in Salesforce, export all labels and messages, in excel format, sent it to translation and import the labels of the new language.    

### Adding Spanish Language Method1:     
1. Change the metadata structure, adding additional 2 fields: StatusLabel_es and StatusMessage_es
| Code     |      Name     |  StatusLabel |StatusLabel_fr  |  StatusLabel_it   |  StatusLabel_es   |  StatusMessage    |  StatusMessage_fr |  StatusMessage_it |  StatusMessage_es |
|----------|:------------- |:-------------|:---------------|:------------------|:------------------|:------------------|:------------------|:------------------|:------------------|
| TRS1     | Trans 1       | Initial      | Initiale       |Iniziale           |Inicial            | Step              | Etape             | Fare un passo     | Paso              |

2. Change APEX Classe Codes to take into consideration the new language


Method2:    
Nothing to do    


APEX CLASS for Method1:


APEX CLASS for Method2:

Add function  translate in DICE_Utilities



