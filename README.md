[![DOI](https://zenodo.org/badge/1225600379.svg)](https://doi.org/10.5281/zenodo.20054328)

# Urban-Mobility-Ontology

**Version 1.0.0 · License: CC-BY 4.0**

A semantic knowledge base for urban mobility and public transportation, with a
specific focus on **Demand-Responsive Transport (DRT)** services operated by
autonomous shuttles.

---

## 1. Overview

This repository provides an OWL/RDF ontology designed as a semantic knowledge
base for integrating heterogeneous mobility data, including:

- demand-responsive transport requests and passenger information;
- regular public transportation services based on GTFS;
- urban infrastructure and the road network;
- spatial information based on GeoSPARQL;
- temporal information based on OWL-Time;
- events, disruptions, and their impacts on transportation services and infrastructure.

The main objective is to provide a generic, shared, interoperable and extensible
semantic model for urban mobility systems, particularly DRT. It can be used to
facilitate data integration, reasoning, decision support, optimization and the
explainability of decisions for the management of public transport services.

The repository contains both the **schema (TBox)** and a **populated knowledge
base (ABox)** instantiated from real data of the La Rochelle / Charente-Maritime
area (OpenStreetMap, GTFS, real DRT reservations) plus a controlled set of
simulated disruption events.

---

## 2. Namespaces and prefixes

| Prefix | IRI | Role |
|---|---|---|
| `DRT:` | `http://www.semanticweb.org/hp/ontologies/2024/6/OnDemand#` | DRT demand core (**introduced**) |
| `GTFS:` | `http://www.semanticweb.org/hp/ontologies/2024/transport#` | GTFS-based transport service layer (**introduced**) |
| `Infrastructure:` | `http://www.semanticweb.org/hp/ontologies/2024/7/Modélisation#` | Urban infrastructure layer (**introduced**) |
| `sem:` | `http://semanticweb.cs.vu.nl/2009/11/sem/` | Simple Event Model (**reused + extended**) |
| `dtx:` | `http://purl.org/td/transportdisruption#` | Transport Disruption Ontology (**reused, fragment**) |
| `geos:` | `http://www.opengis.net/ont/geosparql#` | GeoSPARQL (**reused**) |
| `time:` | `http://www.w3.org/2006/time#` | OWL-Time (**reused**) |

---

## 3. Ontology modules

| File | Module | Contains |
|---|---|---|
| `DRT.rdf` | DRT core + full populated KB | demand concepts and instance of the integrated graph |
| `Urban_infrastructure.rdf` | Infrastructure | streets, road segments, intersections, RondAbout, Road_marking, etc  |
| `GTFS.zip` | GTFS service | scheduled-service data (stops, routes, trips, stop-times, booking rules, etc) |
| `event_sem.rdf` | Event | SEM core + the `DRT:PlaceImpact` extension |
| `DisruptiveOntology.rdf` | Disruption | Dtx fragment (disruption types, impacts, plans) |
| `geo.rdf` | Spatial | GeoSPARQL vocabulary |
| `owltime.rdf` | Temporal | OWL-Time vocabulary |

### 3.1 DRT demand core (`DRT:`)

The central element of the ontology: demand-responsive requests and their
interaction with the urban environment, transport services, spatio-temporal
constraints and unforeseen events.

| Class | Meaning |
|---|---|
| `DRT:Reservation` | A demand-responsive booking. Central entry point of the demand layer. |
| `DRT:Ride` | Describe a complete shuttle journey that combines several passenger trips. |
| `DRT:Trips` | A single passenger leg (one pickup → one drop-off) belonging to a ride. |
| `DRT:Passenger` | The person actually transported on a trip. |
| `DRT:Customer` | The account holder who makes reservations (may differ from the passenger). |
| `DRT:Driver` | The shuttle driver. |
| `DRT:Admin` | Administrative actor. |

### 3.2 Urban infrastructure (`Infrastructure:`)

Describes the physical environment in which the service operates, at three levels
of granularity.

| Level | Classes |
|---|---|
| **Micro** | `Streets`, `Road_segment`, `Intersection`, `RondAbout`, `Sidewalk`, `Bicycle_lane`, `Pedestrian_crossing`, `Road_markings`, `Arrow_markings`, `Parking_markings`, `Traffic_light`, `Traffic_signs`, `Traffic_control`, `Obstacles`, `vehicle`, `Cars`, `bicycle`, `Bus`, `Shuttle`, `DRT_Shuttle`, `Pedestrians`, `Charging_station`, `Parking`, `Building`. |
| **Meso** | `Neighborhood`, `AreaOfInterest`, `CommercialArea`, `LeisureArea`, `Industrial_Zone`, `CampusArea`, `CityCenter`, `School`, `Hospital`, `Point_POI`. |
| **Macro** | `Municipalities`. |
| Granularity markers | `Micro`, `Meso`, `Macro`. |

### 3.3 GTFS service layer (`GTFS:`)

Represents scheduled public transport services and ensures interoperability
between fixed-route services and DRT. GTFS data are provided in `GTFS.zip`.

Standard GTFS entities, including: `GTFS:Agency`, `GTFS:Routes`, `GTFS:Trips`,
`GTFS:Stops`, `GTFS:StopTimes`, `GTFS:Shapes`, `GTFS:Calendar`,
`GTFS:CalendarDates`, `GTFS:Frequency`, `GTFS:BookingRule`, `GTFS:Pathway`,
`GTFS:Transfer`, `GTFS:Network`, `GTFS:Area`, `GTFS:Level`, `GTFS:Location`,
`GTFS:FareAttribute`, `GTFS:FareRule`, `GTFS:FareProduct`, `GTFS:FareMedia`,
`GTFS:FareLegRule`, `GTFS:FareTransferRule`, `GTFS:Attribution`,
`GTFS:Translation`, `GTFS:TimeFrame`.

### 3.4 Event and disruption layer (`sem:` + `dtx:`)

| Class | Meaning |
|---|---|
| `sem:Event` | Generic event. |
| `dtx:DisruptiveEvent` ⊑ `sem:Event` | A transport-disrupting event. |
| `sem:Impact` | Generic consequence of an event. |
| `dtx:DisruptiveImpact` ⊑ `sem:Impact` | Impact on a traveller's plan/trip. |
| `DRT:PlaceImpact` ⊑ `sem:Impact` *(introduced)* | Impact on a physical place (road segment, stop, street). |
| `sem:Place`, `sem:Actor`, `sem:Time`, `sem:EventType` | Generic SEM context entities. |

### 3.5 Spatial and temporal layers

`geo.rdf` provides the GeoSPARQL vocabulary (spatial representation) and
`owltime.rdf` provides the OWL-Time vocabulary (temporal representation). Both are
reused as reference vocabularies.

---

## 4. Reused vs. aligned vs. introduced

This table makes explicit, for each external standard, what was taken and what is
new — addressing the most common question about the resource's contribution.

| Source | Status | What is taken / added |
|---|---|---|
| **GeoSPARQL** | Reused (reference vocabulary) | `geos:Feature`, `geos:Geometry`, `geos:hasGeometry`, `geos:hasDefaultGeometry`, `geos:asWKT`, topological relations (`geos:sfTouches`, …). Infrastructure entities are declared as `geos:Feature`. |
| **OWL-Time** | Reused (reference vocabulary) | `time:Instant`, `time:Interval`, `time:hasBeginning`, `time:hasEnd`, `time:inDateTime`. Used for reservation, trip and event time. |
| **SEM** | Reused **and extended** | Generic event layer (`sem:Event`, `sem:Place`, `sem:Actor`, `sem:Impact`, `sem:hasPlace`, `sem:hasTime`, `sem:eventType`). **Introduced:** `DRT:PlaceImpact` and `DRT:ImpactOnPlace` to represent infrastructure-oriented impacts. |
| **Transport Disruption (Dtx)** | Reused (fragment) | `dtx:DisruptiveEvent`, `dtx:DisruptiveImpact`, the disruption-type hierarchy, `dtx:causeOf`, `dtx:hasCause`, `dtx:impactsOn`, `dtx:Plan`. |
| **GTFS service layer** (`GTFS:`) | Introduced (standard-aligned) | An OWL rendering of the GTFS specification (Agency, Routes, Trips, Stops, StopTimes, BookingRule, Fare\*, Calendar, …) for interoperability with fixed-route services. |
| **Urban infrastructure** (`Infrastructure:`) | Introduced | Micro/meso/macro road-network model: `Streets`, `Road_segment`, `Intersection`, `RondAbout`, Road_markings,etc. |
| **DRT demand core** (`DRT:`) | Introduced | `Reservation`, `Ride`, `Trips`, `Passenger`, `Customer`, `Driver`, and their operational attributes. |

---


## 5. How to use the ontology

**With Protégé**

1. Download this repository.
2. Open Protégé.
3. Load `DRT.rdf` (it imports the other modules).
4. If imports are not resolved automatically, also load
   `Urban_infrastructure.rdf`, `DisruptiveOntology.rdf`, `event_sem.rdf`,
   `geo.rdf`, `owltime.rdf`, and the GTFS data from `GTFS.zip`.
5. Run a reasoner (HermiT or Pellet) to check consistency.
6. Explore the classes, object properties, data properties and individuals.

**Querying**

The `queries.sparql` file contains SPARQL queries ready to be executed.

---


## 6. Governance, sustainability and citation

- **Maintenance.** The resource is maintained in the context of the **YeloFLEX**
  DRT project (La Rochelle), which provides the application context and continuity.
- **License.** Creative Commons Attribution 4.0 (CC-BY 4.0).

```bibtex
@software{elgadi_urban_mobility_ontology_2026,
  author    = {El Gadi Nourelhouda, Talhi Esma and Bouju Alain},
  title     = {Urban Mobility Ontology: A Semantic Knowledge Base for
               Demand-Responsive Public Transport Management},
  version   = {1.0.0},
  year      = {2026},
  publisher = {Zenodo},
  doi       = {10.5281/zenodo.20054328},
  url       = {https://doi.org/10.5281/zenodo.20054328}
}
```
