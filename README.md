# S2.03.MongoDB.Lv2.Ex1

### 🍕 Projecte Comandes de Menjar a Domicili – Modelatge amb MongoDB
Aquest projecte té com a objectiu dissenyar la base de dades per a una web de comandes de menjar a domicili, centrant-se en un model documental amb MongoDB. El sistema permet gestionar clients, comandes, productes, botigues i empleats/des d’una manera flexible i escalable.

### 📚 Visió General
La base de dades cobreix les següents àrees funcionals:

Gestió de clients i les seves comandes

Gestió de productes (pizzes, hamburgueses i begudes)

Informació de botigues i empleats/des

Assignació de comandes a botigues i repartidors

Control de recollida o repartiment a domicili

### 📂 Estructura del Model
### 🧍 Col·lecció: clients
Cada document representa un client:

```
{
  "_id": "cli001",
  "nom": "Júlia",
  "cognoms": "Martínez López",
  "adreça": "Carrer Gran, 25",
  "codi_postal": "08001",
  "localitat": "Barcelona",
  "provincia": "Barcelona",
  "telefon": "612345678"
}
```

### 🛍️ Col·lecció: comandes
Cada comanda és única i vinculada a un client i una botiga:

```
{
  "_id": "com123",
  "client_id": "cli001",
  "botiga_id": "bot001",
  "data_hora": "2025-06-03T20:15:00Z",
  "tipus": "domicili",  // o "recollida"
  "productes": [
    { "producte_id": "prd001", "quantitat": 2 },
    { "producte_id": "prd005", "quantitat": 1 }
  ],
  "preu_total": 27.50,
  "nota": "Sense formatge a la pizza, si us plau.",
  "repartidor": {
    "empleat_id": "emp004",
    "nom": "David Roca",
    "data_hora_lliurament": "2025-06-03T20:45:00Z"
  }
}
```

### 🍔 Col·lecció: productes
Els productes poden ser pizzes, hamburgueses o begudes. Les pizzes poden tenir categoria.

```
{
  "_id": "prd001",
  "tipus": "pizza",
  "nom": "Pizza 4 formatges",
  "descripcio": "Mozzarella, gorgonzola, parmesà, roquefort",
  "imatge": "url_o_nom_imatge.jpg",
  "preu": 11.50,
  "categoria": "Especialitats d'estiu"
}

{
  "_id": "prd005",
  "tipus": "beguda",
  "nom": "Coca-Cola 33cl",
  "descripcio": "Refresc amb gas",
  "imatge": "cocacola.jpg",
  "preu": 2.00
}
```

### 🏪 Col·lecció: botigues
Cada botiga gestiona múltiples comandes i té la seva plantilla:

```
{
  "_id": "bot001",
  "adreça": "Av. Diagonal, 456",
  "codi_postal": "08008",
  "localitat": "Barcelona",
  "provincia": "Barcelona"
}
```

### 👷 Col·lecció: empleats
Cada empleat treballa en una sola botiga i pot ser cuiner/a o repartidor/a:

```
{
  "_id": "emp004",
  "nom": "David",
  "cognoms": "Roca Vidal",
  "nif": "12345678Z",
  "telefon": "667778889",
  "rol": "repartidor",
  "botiga_id": "bot001"
}
```

### 🔍 Consultes d’Exemple
🔸 Totes les comandes realitzades per un client:

```
db.comandes.find({ client_id: "cli001" })
```
🔸 Tots els productes de tipus pizza:

```
db.productes.find({ tipus: "pizza" })
```
🔸 Repartidors d’una botiga concreta:

```
db.empleats.find({ rol: "repartidor", botiga_id: "bot001" })
```
🔸 Comandes amb repartiment a domicili:

```
db.comandes.find({ tipus: "domicili" })
```
🔸 Comandes entregades per un repartidor específic:

```
db.comandes.find({ "repartidor.empleat_id": "emp004" })
```

### 🛠️ Eines Utilitzades
MongoDB – Emmagatzematge NoSQL de documents

MongoDB Compass – Visualització i consulta de dades

JSON Schema (opcional) – Validació d’estructures

Visual Studio Code / Studio 3T – Desenvolupament i proves

### 🔗 Repositori GitHub
https://github.com/ArnauAsole/S2.03.MongoDB.Lv2.Ex1.git
