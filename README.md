## urban-mobility-ontology

## Overview
This repository provides an OWL/RDF ontology for urban mobility and public transportation, with a specific focus on Demand-Responsive Transport (DRT) services.

The ontology is designed as a semantic knowledge base for integrating heterogeneous mobility data, including:

- demand-responsive transport requests and passenger information

- Regular public transportation services based on GTFS

- Urban infrastructure and the road network

- Spatial information based on GeoSPARQL

- Temporal information based on OWL-Time

- Events, disruptions, and their impacts on transportation services and infrastructure.

The main objective of this ontology is to provide a generic, shared, interoperable, and extensible semantic model for urban mobility systems, particularly demand-responsive transport (DRT). It can be used to facilitate data integration, reasoning, decision support, optimization and explainability of decisions for the management of public transport services.

## Ontology Modules

## 1. DRT Ontology

The DRT.rdf file contains the basic model of on-demand transportation.

It represents concepts such as: reservations, passengers, trips, pick-up and drop-off locations, etc

This module is the central element of the ontology. It allows for the representation of demand-responsive transport requests and their interactions with the urban environment, transportation services, spatio-temporal constraints, and unforeseen events.

## 2. Urban Infrastructure Ontology

The Urban_infrastructure.rdf file describes the physical environment in which the transport service operates.

It includes concepts related to: streets, road segments, intersections,
municipalities, neighborhoods, etc

The infrastructure model supports different spatial levels of granularity:

micro level: streets, road segments, intersections;
meso level: neighborhoods and areas of interest;
macro level: municipalities and larger territorial entities.
This module allows for the description of the operational context of public transportation services.

## 3. GTFS Ontology

The GTFS.zip file contains GTFS-related data used to represent scheduled public transport services.

The GTFS-based model includes concepts such as: stops, routes, trips, stop times, booking rules, etc

This module supports interoperability between demand-responsive transport and regular public transport services.

## 4. Event and Disruption Ontology

The files event_sem.rdf and DisruptiveOntology.rdf describe events and disruptions that may affect the transport system.

This part of the ontology represents: events, disruptive events, event locations, event duration, impacts on trips or infrastructure, etc 

## 5. Spatial and Temporal Models

The repository also includes reused or aligned ontology files:

geo.rdf: spatial representation based on GeoSPARQL;
owltime.rdf: temporal representation based on OWL-Time.


## How to Use the Ontology
1- Download  this repository

2- Open Protégé

3- Load the DRT.RDF file

4- import the other ontology modules: Urban_infrastructure.rdf, DisruptiveOntology.rdf, event_sem.rdf, geo.rdf, owltime.rdf

5- Explore the classes, object properties, data properties, and individuals.
