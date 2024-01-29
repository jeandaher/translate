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


### APEX Class for Method1:    
```.js
public static Map<String, transco__mdt> getTransco() {
   Map<String, transco_mdt> mcs = transco__mdt.getAll();
   for (transco_mdt row: transco__mdt.getAll()) {
      ...
        switch on (language) {
            when 'en' {
                row.statusLabel = row.statusLabel;
                row.statusMessage = row.statusMessage;
            }
            when 'fr' { 
                row.statusLabel = row.statusLabel_fr;
                row.statusMessage = row.statusMessage_fr;
            }
            when 'it' { 
                row.statusLabel = row.statusLabel_it;
                row.statusMessage = row.statusMessage_it;
            }
        }
      ...
    }  
   }
   return mcs;
}
```


### APEX Class for Method2:  

Add function  translate in DICE_Utilities
```.js
public static String translate(String labelName, String language, String defaultLabel) {
   return Label.translationExists('', labelName, language)
      ? Label.get('', labelName, language)
      : defaultLabel;
}
```

```.js
public static Map<String, transco__mdt> getTransco() {
   Map<String, transco_mdt> mcs = transco__mdt.getAll();
   for (transco_mdt row: transco__mdt.getAll()) {
      ...   
       row.statusLabel = translate('TRANS_STATUS_LABEL', anguage,row.statusLabel);
       row.statusMessage = translate('TRANS_STATUS_MESSAGE', anguage,row.statusMessage);
      ...
    }         
   }
   return mcs;
}

```


### Use Case, adding Spanish Language !    

The procedure in Salesforce, export all labels and messages, in excel format, sent it to translation and import the labels of the new language.    

### Adding Spanish Language Method1:     
1. Change the metadata structure, adding additional 2 fields: StatusLabel_es and StatusMessage_es
   
| Code     |      Name     |  StatusLabel |StatusLabel_fr  |  StatusLabel_it   |  StatusLabel_es   |  StatusMessage    |  StatusMessage_fr |  StatusMessage_it |  StatusMessage_es |
|----------|:------------- |:-------------|:---------------|:------------------|:------------------|:------------------|:------------------|:------------------|:------------------|
| TRS1     | Trans 1       | Initial      | Initiale       |Iniziale           |Inicial            | Step              | Etape             | Fare un passo     | Paso              |

2. Change APEX Classe Codes to take into consideration the new language 'es'    

            when 'es' { 
                row.statusLabel = row.statusLabel_es;
                row.statusMessage = row.statusMessage_es;
            }


### Adding Spanish Language Method2:    
Nothing to do    






