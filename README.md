
![Brief-4](Brief-4.jpg "Brief-4")
# BRIEF 3
## Votre collègue vous demande une code review pour une nouvelle API qu'il vient de coder


# # Code review

Bonjour **Anatole**,

Votre script semble bien structuré et suit les bonnes pratiques pour construire un service FastAPI. Cependant, voici quelques suggestions d’amélioration :

1.  **Validation des paramètres de chemin (Path) :** Pour améliorer la validation des paramètres de chemin, vous pouvez utiliser les outils de validation de FastAPI. Par exemple, vous pouvez définir `year` comme `int` plutôt que `str` avec une validation distincte, et vous pouvez également définir des contraintes sur les valeurs acceptables. Cela peut être fait avec les classes de validation de FastAPI comme `Path`.
    
2.  **SQL Injection :** Votre script semble vulnérable aux attaques par injection SQL. Vous devriez utiliser des requêtes paramétrées pour empêcher ces attaques. Dans votre cas, utilisez `?` pour les paramètres de requête au lieu de formatter les chaînes directement.
    
3.  **Documentation :** Ajoutez des commentaires appropriés à votre script, surtout pour expliquer la logique métier de chaque endpoint.
    
4.  **Connexion à la base de données :** Assurez-vous de gérer correctement la connexion et la fermeture de la connexion à la base de données. Vous pouvez envisager d’utiliser un gestionnaire de contexte (`with`) pour la connexion à la base de données.
    
5.  **Tests unitaires :** Écrivez des tests unitaires pour chaque endpoint. Cela garantira que votre API fonctionne correctement et vous permettra d’identifier rapidement tout problème lors de futures modifications.
    
6.  **Utilisation de variables de configuration :** Si possible, définissez la chaîne de connexion à la base de données et d’autres paramètres dans une configuration externe plutôt que de les codifier directement dans le script.
    

Voici un exemple de modifications pour la validation des paramètres et la prévention de l’injection SQL :

python code

```

`from fastapi import Path`

`# ...`

`# User story 1`
`@app.get("/revenu_fiscal_mo	yen/{city}", description="Renvoie le revenu fiscal moyen de l'année la plus récente pour une ville donnée")`
`async def revenu_fiscal_moyen(city: str = Path(..., title="Ville")):`
  `query = "SELECT revenu_fiscal_moyen FROM foyers_fiscaux ff WHERE ville = ? ORDER BY date DESC LIMIT 1"`
  `return execute_sql(con, query, (city.capitalize(),))`

```

Cordialement,  
Olivier,


