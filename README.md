# Hackathon 
*Groupe 13*

---
### Documentation de l'API

Nous utiliserons cet [**URL de base**](https://31v0z6iw4g.execute-api.eu-west-3.amazonaws.com/prod/hackathon)

**Resources disponibles:**
1. Récupération des couts journalier

    1. Tous les couts journaliers
    - Methode: `POST`
    - URL: `https://31v0z6iw4g.execute-api.eu-west-3.amazonaws.com/prod/hackathon`
    - Headers: 
        - `Content-Type: application/json`
        - `X-Amz-Target: AWSInsightsIndexService.GetCostAndUsage`
    - Payload:
    ```jsonc
    {
        // Format de la date: "yyyy-mm-dd"
        "TimePeriod": {
            // Début de la période à récupérer (min: 2022-01-01)
            "Start": "[DATE]", 
            // Fin de la période à récupérer (max: 2022-03-31)
            "End": "[DATE]"
        }
    }
    ```

    2. Couts journaliers par services AWS
    - Methode: `POST`
    - URL: `https://31v0z6iw4g.execute-api.eu-west-3.amazonaws.com/prod/hackathon`
    - Headers: 
        - `Content-Type: application/json`
        - `X-Amz-Target: AWSInsightsIndexService.GetCostAndUsage`
    - Payload:
    ```jsonc
    {
        // Format de la date: "yyyy-mm-dd"
        "TimePeriod": {
            // Début de la période à récupérer
            "Start": "[DATE]", 
            // Fin de la période à récupérer
            "End": "[DATE]"
        },
        "GroupBy" : [
            {
                "Type" : "TAG",
                "Key" : "[TAG_NAME]"
            }
        ]
    }
    ```

    3. Couts journaliers par tags

2. Récupération des tags
    - Methode: `POST`
    - URL: `https://31v0z6iw4g.execute-api.eu-west-3.amazonaws.com/prod/hackathon`
    - Headers: 
        - `Content-Type: application/json`
        - `X-Amz-Target: AWSInsightsIndexService.GetTags`