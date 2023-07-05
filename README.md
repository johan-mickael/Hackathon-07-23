# Hackathon 
*Groupe 13*

---
### 📝 Documentation de l'API

**✅ Resources disponibles :**

Pour chaque appel API, on utilisera en commun ces options:
- ➡️ Method: `POST`
- ➡️ Base URL: `https://31v0z6iw4g.execute-api.eu-west-3.amazonaws.com/prod/hackathon`
- ➡️ Headers: `Content-Type: application/json`

1. Récupération des couts journalier
- Headers: `X-Amz-Target: AWSInsightsIndexService.GetCostAndUsage`
- Payload (*commun pour les couts journaliers*):
    ```jsonc
    {
        // Format de la date: "yyyy-mm-dd"
        "TimePeriod": {
            // Début de la période à récupérer (min: 2022-01-01)
            "Start": "[START_DATE_PERIOD]", 
            // Fin de la période à récupérer (max: 2022-03-31)
            "End": "[END_DATE_PERIOD]"
        }
    }
    ```
    1. Tous les couts journaliers
    - Response sample
     ```jsonc
    {
        "ResultsByTime": [
            {
                "TimePeriod": {
                    "Start": "[START_DATE_PERIOD]",
                    "End": "[END_DATE_PERIOD]"
                },
                "Total": {
                    "BlendedCost": {
                        // variable selon le service
                        "Amount": [AMOUNT],
                        // USD|EUR|..etc
                        "Unit": "[UNIT]"
                    }
                },
                "Estimated": false
            },
            // ...
        ]
    }
    ```

    2. Couts journaliers par services AWS
    - Payload:
    ```jsonc
    {
        // mettre les payload communs ici (*TimePeriod*)
        "GroupBy" : [
            {
                "Type" : "DIMENSION",
                "Key" : "SERVICE"
            }
        ]
    }
    ```
    - Response sample
    ```jsonc
    {
        "GroupDefinitions": [
            {
                "Type": "DIMENSION",
                "Key": "SERVICE"
            }
        ],
        "ResultsByTime": [
            {
                "TimePeriod": {
                    "Start": "[START_DATE_PERIOD]",
                    "End": "[END_DATE_PERIOD]"
                },
                "Total": {},
                "Groups": [
                    {
                        "Keys": [
                            "An AWS service"
                        ],
                        "Metrics": {
                            "BlendedCost": {
                                // variable par services
                                "Amount": [AMOUNT],
                                // USD|EUR|...etc
                                "Unit": "[UNIT]"
                            }
                        }
                    },
                    // ...
                ]
            }
        ]
    }
    ```

    3. Couts journaliers par tags
    - Payload:
    ```jsonc
    {
        // mettre les payload communs ici (*TimePeriod*)
        "GroupBy" : [
            {
                "Type" : "TAG",
                // Developement|Production
                "Key" : "[TAG_NAME]"
            }
        ]
    }
    ```
    - Response sample
    ```jsonc
    {
        "GroupDefinitions": [
            {
                "Type": "TAG",
                "Key": "[TAG_NAME]"
            }
        ],
        "ResultsByTime": [
            {
                "TimePeriod": {
                    "Start": "[START_DATE_PERIOD]",
                    "End": "[END_DATE_PERIOD]"
                },
                "Total": {},
                "Groups": [
                    {
                        "Keys": [
                            "[TAG_NAME]"
                        ],
                        "Metrics": {
                            "BlendedCost": {
                                // variable selon les services
                                "Amount": [AMOUNT],
                                // USD|EUR|..etc
                                "Unit": "[UNIT]"
                            }
                        }
                    }
                ],
                "Estimated": false
            },
            // ...
        ]
    }
    ```

2. Récupération des tags
- Headers: `X-Amz-Target: AWSInsightsIndexService.GetTags`
- Response sample:
```jsonc
{
    "Tags": [
        "Developement",
        "Production",
        // ...
    ],
    // Nombre de tags retournés (si on a une pagination)
    "ReturnSize": [RETURN_SIZE],
    // Nombre total de tags stockés
    "TotalSize": [TOTAL_SIZE]
}
```