
# Cypher Script to Convert the Article to Neo4j Knowledge Graph

### Here Are The Steps:

1. Wipes the graph clean
2. Creates **nodes** with clean labels & properties
3. Adds **relationships** normalized by role
4. Adds **schema constraints**
5. Sample **Visualization Queries**

---

### The **all-in-one Cypher scripts**:


## **1️⃣ Reset the graph**

```
// Delete everything
MATCH (n) DETACH DELETE n;
```

---

## **2️⃣ Create core nodes**

```
// ---------- PEOPLE ----------
MERGE (sam:Person {name: "Sam Altman"})
  SET sam.bio = "Co-founder of Merge Labs, CEO of OpenAI";

MERGE (alex:Person {name: "Alex Blania"})
  SET alex.bio = "Co-founder of Merge Labs, CEO of Worldcoin";

MERGE (elon:Person {name: "Elon Musk"})
  SET elon.bio = "Founder of Neuralink, CEO of xAI, Tesla, SpaceX";

// ---------- ORGANIZATIONS ----------
MERGE (mergeLabs:Organization {name: "Merge Labs"})
  SET mergeLabs.type = "Brain-Computer Interface Startup",
      mergeLabs.valuation = 850000000,
      mergeLabs.fundraising_target = 250000000,
      mergeLabs.founded = 2025,
      mergeLabs.status = "Early Stage";

MERGE (neuralink:Organization {name: "Neuralink"})
  SET neuralink.type = "Brain-Computer Interface Company",
      neuralink.valuation = 9000000000,
      neuralink.founded = 2016,
      neuralink.status = "Human Trials Underway";

MERGE (openai:Organization {name: "OpenAI"})
  SET openai.type = "Artificial Intelligence Company";

MERGE (worldcoin:Organization {name: "Worldcoin"})
  SET worldcoin.type = "Digital Identity Project";

MERGE (xai:Organization {name: "xAI"})
  SET xai.type = "Artificial Intelligence Company";

MERGE (tesla:Organization {name: "Tesla"})
  SET tesla.type = "Electric Vehicle & Energy Company";

MERGE (spacex:Organization {name: "SpaceX"})
  SET spacex.type = "Aerospace Manufacturer & Space Transport";

// ---------- TECHNOLOGY ----------
MERGE (bci:Technology {name: "Brain-Computer Interface", abbreviation: "BCI"});

// ---------- SECTOR ----------
MERGE (neuro:Sector {name: "Neurotechnology"});
```

---

## **3️⃣ Create normalized relationships**

```
// Sam Altman
MATCH (sam:Person {name: "Sam Altman"}), 
      (merge:Organization {name: "Merge Labs"}), 
      (openai:Organization {name: "OpenAI"})
MERGE (sam)-[:CO_FOUNDED]->(merge)
MERGE (sam)-[:CEO_OF]->(openai);

// Alex Blania
MATCH (alex:Person {name: "Alex Blania"}), 
      (merge:Organization {name: "Merge Labs"}), 
      (worldcoin:Organization {name: "Worldcoin"})
MERGE (alex)-[:CO_FOUNDED]->(merge)
MERGE (alex)-[:CEO_OF]->(worldcoin);

// Elon Musk
MATCH (elon:Person {name: "Elon Musk"}), 
      (neuralink:Organization {name: "Neuralink"}),
      (xai:Organization {name: "xAI"}),
      (tesla:Organization {name: "Tesla"}),
      (spacex:Organization {name: "SpaceX"})
MERGE (elon)-[:FOUNDED]->(neuralink)
MERGE (elon)-[:CEO_OF]->(xai)
MERGE (elon)-[:CEO_OF]->(tesla)
MERGE (elon)-[:CEO_OF]->(spacex);

// Orgs → Technology → Sector
MATCH (merge:Organization {name: "Merge Labs"}), 
      (neuro:Sector {name: "Neurotechnology"}),
      (bci:Technology {name: "Brain-Computer Interface"})
MERGE (merge)-[:OPERATES_IN]->(neuro)
MERGE (merge)-[:USES_TECHNOLOGY]->(bci);

MATCH (neuralink:Organization {name: "Neuralink"}), 
      (neuro:Sector {name: "Neurotechnology"}),
      (bci:Technology {name: "Brain-Computer Interface"})
MERGE (neuralink)-[:OPERATES_IN]->(neuro)
MERGE (neuralink)-[:USES_TECHNOLOGY]->(bci);
```

---

## **4️⃣ Add schema constraints**

```
CREATE CONSTRAINT unique_person_name IF NOT EXISTS
FOR (p:Person) REQUIRE p.name IS UNIQUE;

CREATE CONSTRAINT unique_org_name IF NOT EXISTS
FOR (o:Organization) REQUIRE o.name IS UNIQUE;

CREATE CONSTRAINT unique_sector_name IF NOT EXISTS
FOR (s:Sector) REQUIRE s.name IS UNIQUE;

CREATE CONSTRAINT unique_tech_name IF NOT EXISTS
FOR (t:Technology) REQUIRE t.name IS UNIQUE;
```

---

## **5️⃣ Visualization Queries**

**Quick check query**

```
MATCH (n)-[r]->(m) 
RETURN n, r, m;
```

## **visualization-friendly Cypher**

Visualization-friendly Cypher that will lay out your graph so you can instantly see:
- People in one cluster
- Organizations connected to them
-Technologies & Sectors connected from organizations

It uses RETURN with aliases so Neo4j Browser shows a nice force-directed layout.

```
// This pulls the whole graph but keeps clusters visually distinct
MATCH (p:Person)-[r1]->(o:Organization)
OPTIONAL MATCH (o)-[r2]->(t:Technology)
OPTIONAL MATCH (o)-[r3]->(s:Sector)
RETURN p, r1, o, r2, t, r3, s;
```

---