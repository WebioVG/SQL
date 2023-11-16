## 10 Listez pour chaque ticket la quantité totale d’articles vendus. (Classer par quantité décroissante)

```mysql
SELECT NUMERO_TICKET, SUM(QUANTITE) as quantite
FROM ventes
GROUP BY NUMERO_TICKET
ORDER BY quantite DESC
```

## 11 Listez chaque ticket pour lequel la quantité totale d’articles vendus est supérieure à 500. (Classer par quantité décroissante)

```mysql
SELECT NUMERO_TICKET, SUM(QUANTITE) as quantite
FROM ventes
GROUP BY NUMERO_TICKET
HAVING quantite > 500
ORDER BY quantite DESC
```

## 12 Listez chaque ticket pour lequel la quantité totale d’articles vendus est supérieure à 500. On exclura du total, les ventes ayant une quantité supérieure à 50 (classer par quantité décroissante)

```mysql
SELECT NUMERO_TICKET, SUM(QUANTITE) as quantite
FROM ventes
WHERE QUANTITE <= 50
GROUP BY NUMERO_TICKET
HAVING quantite > 500
ORDER BY quantite DESC
```

## 13 Listez les bières de type ‘Trappiste’. (id, nom de la bière, volume et titrage)

```mysql
SELECT ID_ARTICLE, NOM_ARTICLE, VOLUME, TITRAGE, NOM_TYPE
FROM article
JOIN type ON article.ID_ARTICLE = article.ID_ARTICLE
WHERE NOM_TYPE = "Trappiste"
```

## 14 Listez les marques de bières du continent ‘Afrique’

```mysql
SELECT ID_MARQUE, NOM_MARQUE, NOM_CONTINENT
FROM marque
JOIN pays ON marque.ID_PAYS = pays.ID_PAYS
JOIN continent ON pays.ID_CONTINENT = continent.ID_CONTINENT
WHERE NOM_CONTINENT = "Afrique"
```

## 15 Lister les bières du continent ‘Afrique’

```mysql
SELECT ID_ARTICLE, NOM_ARTICLE, NOM_CONTINENT
FROM article
JOIN marque ON article.ID_MARQUE = marque.ID_MARQUE
JOIN pays ON marque.ID_PAYS = pays.ID_PAYS
JOIN continent ON pays.ID_CONTINENT = continent.ID_CONTINENT
WHERE NOM_CONTINENT = "Afrique"
```

## 16. Lister les tickets (année, numéro de ticket, montant total payé). En sachant que le prix de vente est égal au prix d’achat augmenté de 15%.

```mysql
SELECT  ticket.ANNEE,
		ticket.NUMERO_TICKET,
        SUM(ventes.QUANTITE * article.PRIX_ACHAT * 1.15) as total
FROM ticket
JOIN ventes ON ticket.NUMERO_TICKET = ventes.NUMERO_TICKET
JOIN article ON ventes.ID_ARTICLE = article.ID_ARTICLE
GROUP BY ticket.ANNEE, ticket.NUMERO_TICKET
```

## 17  Donner le C.A. par année.

```mysql
SELECT SUM(ticketsTotal.total)
FROM
(
SELECT  ticket.ANNEE,
		ticket.NUMERO_TICKET,
        SUM(ventes.QUANTITE * article.PRIX_ACHAT * 1.15) as total
FROM ticket
JOIN ventes ON ticket.NUMERO_TICKET = ventes.NUMERO_TICKET
JOIN article ON ventes.ID_ARTICLE = article.ID_ARTICLE
GROUP BY ticket.ANNEE, ticket.NUMERO_TICKET
) as ticketsTotal
```

## 18. Lister les quantités vendues de chaque article pour l’année 2016.

```mysql
SELECT article.NOM_ARTICLE, SUM(ventes.QUANTITE) as total_vendu
FROM ticket
JOIN ventes ON ticket.NUMERO_TICKET = ventes.NUMERO_TICKET
JOIN article ON ventes.ID_ARTICLE = article.ID_ARTICLE
WHERE ticket.ANNEE = "2016"
GROUP BY article.NOM_ARTICLE
```

## 19. Lister les quantités vendues de chaque article pour les années 2014, 2015, 2016.

```mysql
SELECT article.NOM_ARTICLE, SUM(ventes.QUANTITE) as total_vendu
FROM ticket
JOIN ventes ON ticket.NUMERO_TICKET = ventes.NUMERO_TICKET
JOIN article ON ventes.ID_ARTICLE = article.ID_ARTICLE
WHERE ticket.ANNEE IN ("2014", "2015", "2016")
GROUP BY article.NOM_ARTICLE
```

