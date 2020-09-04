# Implementation guidelines for NDE alignment of cultural heritage data management and publication infrastructure

## 0 Introduction
This document describes how IT suppliers can help the Dutch cultural heritage institutions to become more compliant with the principles for cooperation in the Dutch Digital Heritage Network (NDE). It is and will be constructed in full cooperation with suppliers. We ask IT suppliers of data management and publication software to implement the guidelines outlined in this document in their software products. This will help the Dutch heritage institutions in making their information accessible to services and users on the web.

The goal of cooperation in the network is to increase the social value of the cultural heritage information by improving its visibility, usability and sustainability. A crucial part of this challenge is to improve the capabilities of institutions to share their information in the network and to integrate digital heritage information from various sources to build relevant services for their audiences. 

### 0.1 Relation with other documentation
This document builds upon the [high-level functional design](https://github.com/netwerk-digitaal-erfgoed/high-level-design) for the network of cultural heritage information created earlier in the NDE program. In the high level design we define terms, building blocks and functions. The design in itself is based on the [Dutch digital heritage reference architecture (DERA)](https://dera.netwerkdigitaalerfgoed.nl/), the [National Digital Heritage Strategy](https://www.netwerkdigitaalerfgoed.nl/en/about-us/national-digital-heritage-strategy/) and the [NDE position paper](https://www.netwerkdigitaalerfgoed.nl/wp-content/uploads/2018/02/NDE_PositionPaper_NetworkHeritageInformation-EN-v2.pdf).

This document aims to initiate an open discussion and cooperation with the technical partners in the network. The final goal is to document practical solutions that are within reach of the various IT systems used by the institutions and developed by the IT suppliers actively cooperating with NDE. Where appropriate, formal specifications of these solutions will be proposed to the Architecture Board of the DERA to become part of the long term agreements within the cultural heritage domain.

### 0.2 Overview
A large part of the guidelines in this document follows the general practice for publishing [Linked Data](https://en.wikipedia.org/wiki/Linked_data). As stated in the [reference architecture](https://dera.netwerkdigitaalerfgoed.nl/index.php/Linked_Data) (Dutch) Linked Data is regarded a key technology in the cultural heritage domain for integrating the huge amount of information resources within the network. Linked Data is therefore the driver for providing and maintaining coherent digital services within the network.

The object descriptions should be self-contained in respect to identifiers (namely '[Uniform Resource Identifiers](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier)', URIs) and metadata. (see section [1](https://github.com/netwerk-digitaal-erfgoed/cm-implementation-guidelines/#1-publishing-collection-information)). This metadata should contain as much terms as possible (see section [2](https://github.com/netwerk-digitaal-erfgoed/cm-implementation-guidelines/#2-connecting-sources)). The dataset itself should be described as a separate resource with a unique identifier and additional metadata describing the characteristics of the dataset as a whole (see section [3](https://github.com/netwerk-digitaal-erfgoed/cm-implementation-guidelines/#3-publishing-dataset-descriptions)).

### 0.3 Quick access through questions
* [Which data models are recommended?](https://github.com/netwerk-digitaal-erfgoed/cm-implementation-guidelines#11-data-model)
* [Which RDF-serialization is recommended?](https://github.com/netwerk-digitaal-erfgoed/cm-implementation-guidelines#12-rdf-serialization)
* [Which technique is recommended to provide data through the web?](https://github.com/netwerk-digitaal-erfgoed/cm-implementation-guidelines#13-publishing-linked-data)
* [How can I use an internal terminology source?](https://github.com/netwerk-digitaal-erfgoed/cm-implementation-guidelines/#21-using-your-own-terminology-source)
* [How can I use an external terminology source?](https://github.com/netwerk-digitaal-erfgoed/cm-implementation-guidelines/#22-using-standardized-terminology-sources)
* [Which processes and data models are recommended for publishing terminology sources?](https://github.com/netwerk-digitaal-erfgoed/cm-implementation-guidelines/#23-publishing-terminology-sources)
* Which techniques are recommended to provide data through the web?
* Which data models are recommended for publishing dataset information?
* Which techniques are recommended to provide data through the web?
* Which protocols are recommended for persistent identification?
* How are persistent identifiers stored in the database?

### 0.4 About this document
RDF can be published in various serializations. For readability we present examples in turtle serialization, although we recommend other serializations in different situations.

## 1 Publishing collection information
Publishing collection information as Linked Data can be done by transformation of the internal data of the collection management system to a Linked Data publishing format as described by the [Resource Description Framework](https://www.w3.org/TR/rdf11-concepts/) (RDF). The primary focus of the guidelines described in this document is to improve the visibility and interoperability of the heritage collections. These guidelines describe how to create interoperability with Linked Data and do not prescribe which techniques are used to store the data, let alone Linked Data technology within the systems.

### 1.1 Data model
#### 1.1.1 Generic data model
The main goal for publishing the object descriptions as Linked Data is to improve the data integration and visibility in the network. Because the heritage network spans institutions from the library, archive and museum domains, a generic data model that can support general visibility on the web is needed. **In order to support a broader visibility on the web outside the cultural heritage domain, we have chosen to conform to [Schema.org](https://schema.org/).**

Interesting links:
* [https://www.contentking.nl/academy/schema-structured-data/](https://www.contentking.nl/academy/schema-structured-data/) (Dutch)

Thanks to Europeana, most institutions and collection management systems are familiar with Dublin Core. Based on dc, a generic data model for cultural heritage institutions has been defined, the Europeana Data Model (EDM). [Recent investigations](https://github.com/netwerk-digitaal-erfgoed/lod-aggregator) have shown that well-formed schema.org data can be transformed to EDM without significant loss of detail. Schema.org contains properties that are very similar to Dublin Core properties. A complete mapping between schema.org and Dublin Core can be found [here](https://dcmi.github.io/schema.org/).

Interesting links:
* [https://seopressor.com/blog/dublin-core-vs-schemaorg-metadata-comparison/](https://seopressor.com/blog/dublin-core-vs-schemaorg-metadata-comparison/)

Some basic examples for:
* a [photo with Dublin Core properties](example-2.ttl)
* the same [photo with schema.org properties](example-3.ttl)
* a [museum object with schema.org properties](example-4.ttl)
* a [two museum objects with schema.org properties](example-5.ttl), showing different rdf:types

#### 1.1.2 Domain data model
The generic model described above will improve the general visibility of the cultural heritage objects, the terms describing the objects and the datasets in which the objects and terms are grouped. In many cases this will lead to further exploration of these objects. For specific users or communities a deeper understanding of the knowledge in the data will be important. Because of the open structure of Linked Data there is no restriction to simply add another layer of description to the resource. See for [example](example-1.ttl) this object description. So institutions can add extra properties and class definitions to the Linked Data they publish. In general [CIDOC-CRM](http://www.cidoc-crm.org/) (and its derivative [Linked Art](https://linked.art/model/)) can be appropriate for museums. For archives the [RiC-O ontology](https://www.ica.org/standards/RiC/RiC-O_v0-1.html) seems to be promising and for libraries [RDA Elements](https://www.rdaregistry.info/Elements/) or [BIBFRAME](https://www.loc.gov/bibframe/) could be relevant. It is up to the institutions in the separate domains to agree on the use and implementation of these shared standards. Best practices and information about actual implementations will be shared in the network.

#### 1.1.3 Rights
TBD
The DERA requires institutions to publish their metadata with an open license (for some institutions this requirement might still be a challenge). The actual access to the digital object itself can be restricted; additional license statements for use and reuse of the objects should be specified in the metadata. 

### 1.2 RDF serialization
RDF - being the principle to express data in triples - can be formated in various 'serializations'. Different RDF serialization are useful in different situations.

#### 1.2.1 'Traditional' linked data
The oldest type of serialization is RDF/XML. This format is complex and old-fashioned. It could be very useful though in XML ecosystems. The best readable serialization is 'turtle'. Examples in this document are written in this form. Linked data provided in '[n-triples](https://nl.wikipedia.org/wiki/N-Triples)' format can be processed easily in all linked data tooling.

Interesting link:
* [https://ontola.io/blog/rdf-serialization-formats/](https://ontola.io/blog/rdf-serialization-formats/)

In almost all programming languages libraries are available to transform one RDF-serialization into another. Check for libraries in your favorite programming language.

**Please offer your data in at least n-triples format.** See for example [this photo-example](nt-examples/example-3.nt) that we introduced in turtle format earlier.

If triples are published in both the generic and the specific model they are all included in the same data-file.

You could provide more than one serialization and offer the user a choice with 'content negotiation'. (see [1.3.2](https://github.com/netwerk-digitaal-erfgoed/cm-implementation-guidelines#132-web-compliancy-level-resolvable-uris)).

#### 1.2.2 JSON-LD
JSON-LD is the youngest format and comprehensible to webdevelopers that are used to JSON. The format is more difficult to process in native Linked Data environments. We therefore recommend only to use JSON-LD inline in the landing page of an object. (see [1.3.2](https://github.com/netwerk-digitaal-erfgoed/cm-implementation-guidelines#132-web-compliancy-level-resolvable-uris))

### 1.3 Publishing Linked Data
Linked Data can be published in several ways. In this part we will discuss four methods ranging in levels of complexity of implementation. Users could prefer one of these methods to obtain the data for their purpose, so the publication-methods should be offered in parallel.

#### 1.3.1 Basic level: Data dumps
Most of the current collection management systems support XML-based export formats. In many cases a conversion using XSLT Stylesheets is possible to generate a Linked Data dump. The system should support a workflow that can be operated periodically by the system administrator in order to produce the dump. The dump should be described by a dataset description. The link pointing to the dump should be fit for automatic processing and therefore accessible with for instance a ```curl``` command.

A dump could be either a zip-file containing files for every object or one big file containing all the triples. **NDE prefers a datadump in one file containing ntriples.** A file with ntriples can be easily combined from various sources and easily cut into pieces for processing.

In some cases conversion cannot be done by the collection management system itself and a separate publication functionality is required. This can be another system within the institution or a system run by a partner in the network (an aggregator or other service provider). An export in CSV format could for instance be converted into RDF with the [LDWizard](https://github.com/netwerk-digitaal-erfgoed/LDWizard-ErfgoedWizard).

#### 1.3.2 Web compliancy level: resolvable URIs
Although dumps are sufficient to support basic services, proper Linked Data implementations should provide Linked Data per object, in Linked Data terminology called a ‘resource’. Each resource in the collection should have a stable and well-formed URI. This URI should be ‘resolvable’. This means that the webserver provides data about the resource in a format depending on the accept-header in the HTTP request. This functionality is called [content negotiation](https://www.w3.org/Protocols/rfc2616/rfc2616-sec12.html) which enables browsers or other applications to ask for a specific language or representation of the available content. For Linked Data this mechanism is used to differentiate between human-readable content (a rendered HTML page) and machine-readable content (in RDF).

For building real time network services that integrate disparate resources, content negotiation should be in place to serve the Linked Data. In this case creating a dump is no longer necessary as it is possible to describe the dataset as a collection of resolvable URIs.

To improve the overall discoverability on the web it is recommended to add the Schema.org Linked Data format to the landing page of the object on the website. [Google recommends](https://developers.google.com/search/docs/guides/intro-structured-data) doing this by including the Linked Data as [JSON-LD](https://json-ld.org/) in the page. The json-ld file could be provided separately from the webpage and including with a JavaScript-function. See this [example](http://cclod.netwerkdigitaalerfgoed.nl/test.html). 

#### 1.3.3 Advanced level: queryable Linked Data
Instead of building large centralized services NDE envisions a distributed network of empowered organizations that share and reuse their digital information directly. This means that organizations, data providers or service providers, can easily query and combine data from several sources in the network. This satifies two needs.

Firstly it enables users to create a dedicated query for selecting and harvesting specific data. This data could be used to combine in a thematical data-service, eg. Netwerk Oorlogsbronnen. The facility could be used as a more sophisticated endpoint, in addition to an OAI-PMH endpoint or a JSON API.

Secondly this kind of querying could be used dynamically: whenever a user wants to combine data, various endpoints could be approached and results could be combined on-the-fly. This type of querying is still a technological challenge but is already feasible in small-scale applications.

The first step in this direction is to make queryable Linked Data available. This can be done by implementing the SPARQL Query Language supported by so-called triplestore databases. Another, less demanding technology is the use of [Triple Pattern Fragments](https://linkeddatafragments.org/specification/triple-pattern-fragments/). This offers an easy way of querying the available data and is much more scalable but puts a larger burden on the client for processing the query results. 

Further exploration in the area of decentralized querying needs to be done and NDE invites the IT partners to work together on example implementations to determine what practical steps could be made in this direction.

#### 1.3.4 Other considerations for Linked Data publication
Although Linked Data in the core of the collection management systems is not an explicit requirement for NDE it will become more important to reorganize the internal data structure of the systems so that it aligns with the Linked Data principles. This will make the transformation to Linked Data more straightforward and will offer more opportunities to profit from the reuse of external Linked Data. NDE welcomes cooperation with IT partners considering to move in this direction.

Another area that needs further exploration is the handling of multiple layers of object descriptions or enrichments, for example originated from different sources of other institutions, digital humanities research projects or crowdsourcing projects. Keeping track of the provenance of different versions or the ability to maintain and publish different (time) versions of the same resource descriptions (i.e. [Memento](http://timetravel.mementoweb.org/about/), [Web Annotations](https://www.w3.org/TR/annotation-model/)) are other areas where exploration needs to be done. For these topics NDE seeks cooperation with IT partners and with the [CLARIAH-PLUS project](https://www.clariah.nl/), responsible for building research infrastructures in the Digital Humanities domain.

A third development is the concept of ['profile negotiation'](https://www.w3.org/TR/dx-prof-conneg/). Additional to content negotiation in profile negotiation a user can request data according to a certain information model, in our case the generic datamodel or the specific datamodel.

## 2 Connecting sources
"Connected sources" are sources that refer to each other and use each other's information. This is done using terms. Terms are, for example, subjects, persons or places. Each term has a URI as an identifier. Because a URI is a unique webaddress the URI makes unambiguously clear which term is meant. Terms and their URIs are managed in terminology sources, such as thesauri, reference lists or classification systems. Examples are [AAT](https://www.getty.edu/research/tools/vocabularies/aat/), [GeoNames](https://www.geonames.org/) or [WO2 Thesaurus](https://data.niod.nl/WO2_Thesaurus.html) (Dutch).

For connecting sources, it is important that institutions relate URIs of terms to the descriptions of their heritage objects. There are various options for this which are discussed below. The options are increasing in complexity – for example, they require changes to the collection management system – but also provide better functionality.

### 2.1 Using your own terminology source
An institution can create and use its own terminology source. Most of the time a collection management system facilitates the development and maintenance of a thesaurus or set of persons. These sources contain the terms that the collection manager can use when describing heritage objects. This makes it easy to relate terms. A limitation, however, is that the maintenance of ones own source could be cumbersome. Another limitation is that the terms in the source may not be known to users outside the institution. This reduces the ability to connect sources from different institutions.

In the terminology management module of a collection management system the user should be able to relate the internal term to an external one. One could for instance state that the internal term for 'schilderij' is an exact match with the external term 'paintings' in the AAT. Other types of relations are possible, for instance an internal term 'oil-painting' is a narrower term of the AAT 'paintings' (see: [2.3.2](https://github.com/netwerk-digitaal-erfgoed/cm-implementation-guidelines/#232-technology-and-datamodel)) Of course this external term is defined with the proper URI, and stored as such. The process of relating terms form one (internal) terminology source with another (external) one, is called _alignment_.

If a terminology source is developed and used instead of a standardized one, the terminology source apparently has an added value to the field. For that reason the collection management system must be able to publish the terminology source, with alignments, as Linked Data (see: [2.3](https://github.com/netwerk-digitaal-erfgoed/cm-implementation-guidelines/#23-publishing-terminology-sources)).

### 2.2 Using standardized terminology sources
Using terms that are not connected to the network of internationally standardized terminology sources reduces the ability to connect sources from different institutions. We recommend to use as much standardized terms as possible.

#### 2.2.1 Manually searching a terminology source
This is the simplest, low-tech approach to assign the URI of a term to the description of an heritage object. A collection manager goes to the online system of a terminology source and searches for a term, for example 'paintings' in AAT. The manager then copies the URI of the term, goes back to her collection management system and pastes the URI in a designated field. This approach requires few changes to the collection management system: a field has to be created in order to store the URI. On the other hand, this approach is cumbersome: a manager has to perform some actions manually.

#### 2.2.2 Adding terms in bulk
Instead of adding a (URI of a) term to an object description one-by-one, the curator could export the data from her system and add the terms and its URIs in bulk. This could be done with applications like [Open Refine](https://openrefine.org/). For this approach, the collection management system must be able to export the data, for instance in CSV format, and import the new data with its additional link to the term.

The addition of a term can be based on an existing field containing only a string of the data, for instance 'schilderij'. By using search-and-replace kind of tricks the additional link could be added. This type of work is called _reconciliation_.

#### 2.2.3 Importing a terminology source
An institution can import one or more terminology sources into its collection management system, such as AAT and/or WW2 Thesaurus. This makes it easy to use terms: the collection manager can search for terms in her management system, without having to switch to the system of the source, as is the case when searching terms manually (see [2.2.1](https://github.com/netwerk-digitaal-erfgoed/cm-implementation-guidelines/#221-manually-searching-a-terminology-source)). A limitation is that the manager does not use current data: an import takes place periodically – for example: once a day or month – so that changes to the terminology source are not immediately visible.

#### 2.2.4 Searching a terminology source in real time
An institution can query a terminology source in real time in its collection management system. A collection manager first enters a search query in a search field. Next, her management system – on the background – queries the terminology source, retrieves the terms that correspond to the query and presents them to the manager. The manager then chooses the desired term and the management system stores the URI of the chosen term. This ensures that the institution works with current data. However, the implementation of this approach in the management system can entail some difficulties: a connection must be established with the source – or multiple connections, if the institution wants to use multiple sources.

#### 2.2.5 Using the Network of Terms
An institution can use the [Network of Terms](http://demo.netwerkdigitaalerfgoed.nl/termennetwerk/en/faq). The Network of Terms is a search engine for terms: it searches one or more terminology sources in real time. The Network of Terms can be used in a collection management system. A collection manager first enters a search query in a search field. Next, her management system – on the background – queries the Network of Terms, retrieves the terms that correspond to the query and presents them to the manager. The manager then chooses the desired term and the management system stores the URI of the chosen term. This makes it easier to use multiple terminology sources: you only need to connect to the Network of Terms.

#### 2.2.6 Indexing data from the terminology source
If (the URI of) a term is stored, collection managers might be interested in related data in the collection management system, for instance alternative labels, pseudonyms, or labels in different languages. This helps the user of the collection management system to retrieve data from her system. As long as the web of data is not as decentralized as we'd wish (see [1.3.3](https://github.com/netwerk-digitaal-erfgoed/cm-implementation-guidelines/#133-advanced-level-queryable-linked-data)), collection management systems could offer obtaining the needed data via resolving the URI (see [1.3.2](https://github.com/netwerk-digitaal-erfgoed/cm-implementation-guidelines/#132-web-compliancy-level-resolvable-uris)) and store and index the extra data in the database. The related data must be synchronized periodically and the collection management interface must enable to force the synchonization. A collection manager that helps the editors of the standardized source to add or improve data, can than see her results quickly.

## 2.3 Publishing terminology sources
"Published terminology sources" are sources that are important to the cooperating institutions in the Dutch Digital Heritage Network. It enables collection managers to find and use terms in the sources more easily when describing their heritage objects. And that makes digital heritage found easier by data-users.

A terminology source is considered a dataset, with sustainable URIs as described in section 4, described according to the guidelines in section [3](https://github.com/netwerk-digitaal-erfgoed/cm-implementation-guidelines/#3-publishing-dataset-descriptions), and published as dump, with resolvable URIs and in a SPARQL query as described in section [1](https://github.com/netwerk-digitaal-erfgoed/cm-implementation-guidelines/#1-publishing-collection-information).

A terminology source can only be used if it meets a few conditions. Are you the manager of a source and are you considering making it available to the network? Then take the following aspects into account.

### 2.3.1 Authority
Terms are not just ordinary words: they are official notations. The manager of a terminology source guarantees their quality. For example: terms must be accurate and current. Another example: the manager ensures that her terms are permanently available and can be used for a long time. This makes a terminology source an authority on which other institutions can build.

### 2.3.2 Technology and datamodel
A terminology source is used by both humans and machines. For example, institutions' collection management systems must be able to connect to the source. To make this possible, the source must meet certain technological requirements. These requirements follow the Linked Data principles and best practices. This means, for example, that every term in the source gets a sustainable URI; when dereferencing this URI, metadata about the term is returned. **This metadata must be expressed according to a specific RDF metadata model, preferably [Simple Knowledge Organization System (SKOS)](https://www.w3.org/2009/08/skos-reference/skos.html) or Schema.org.** SKOS contains various types of relations, eg. skos:exactMatch, skos:closeMatch or skos:broader to store an alignment between your terminology source and standardized terms.

In addition, terms in the source must be searchable through a SPARQL endpoint. This enables a connection to the Network of Terms. 

### 2.3.3 Cooperation
A terminology source is used by institutions. There is a good chance that these institutions do not use one, but several sources. In order to increase the ease of use of sources, collaboration between source managers and collection managers is essential. For example about the way in which collection managers can propose changes to terms to sources: this should follow a uniform process. Another example: it can happen that two sources define the same term (such as painting). The sources should then jointly agree that these terms have the same meaning and refer to each other's terms – this clarifies the relationship between both terms for collection managers. The collection management system should support these processes.

---

## 3 Publishing dataset descriptions

To increase the findability of datasets of heritage institutions, it is important to publish the dataset descriptions according to a well documented, machine-readable model. When rich dataset descriptions are used, published not only as HTML (for humans) but also as meaningful metadata (for the machine), the findability and use of datasets that heritage institutions make available, will improve.

### Publication model for dataset descriptions
The NDE has drafted a publication model which is based on schema.org. Schema.org is a joint initiative of three major search engines: Bing, Google and Yahoo with the aim of setting up a shared scheme to structure data. Vocabularies from schema.org are developed through an open community process. For datasets, the class https://schema.org/Dataset has been developed. This class is based on W3C DCAT work and benefits from collaboration around the DCAT, ADMS and VoID vocabularies.

See [https://github.com/netwerk-digitaal-erfgoed/project-organisations-datasets/tree/master/publication-model](https://github.com/netwerk-digitaal-erfgoed/project-organisations-datasets/tree/master/publication-model) for the the complete specification of the publication model.

https://netwerk-digitaal-erfgoed.github.io/requirements-datasets/

### How to publish dataset descriptions
For good findability, every dataset description must be accessible via the Internet, must be legible for humans and machines, and use the publication model. The translation of the publication model to a format that can be published and reconstructed later (so that it can be used again) is called serialization (or encoding). The serialization of dataset descriptions can take several forms, JSON-LD is preferred.

Most (automated) users expect to find the metadata in the page itself (inline). Spiders of search engines such as Google might not follow linked JSON-LD files. Even if the linked files (via Javascript) are "injected" into the page, most spiders do not pick up on this. There are more serializations of RDF, such as RDF/XML and Turtle. Spiders of search engines such as Google currently only support microdata, RDFa and JSON-LD. Because search engine findability is an important driver, the use of inline JSON-LD is recommended. However, this does not prevent the additional publication of the dataset description in other serialization formats or a (content negotiation based) separate resource.

### Spreading the knowledge about datasets
The choice for schema.org as a basis for the publication model for dataset descriptions comes with the benefit that this model is known (and used) by big search engines. By adding the dataset description pages to the websites sitemap, search engines are likely to pick up the dataset description and make them available in tools like [Google Dataset Search](https://datasetsearch.research.google.com/).

By registering the datasets with the NDE Register, the network of Dutch heritage institutions can easily find relevant datasets to link with. More generic (open) dataset registers, like data.overheid.nl, can also be used to promote the datasets of the institutions. 

## 4 Duurzame identifiers aangebracht
De webadressen voor objecten op een website van een erfgoedinstelling kunnen om allerlei redenen in de toekomst veranderen. Daarom worden handles geïntroduceerd voor objecten en termen, zodat de verwijzingen die gebruikers maken ook in de toekomst kunnen volgen naar de website en de data, waar deze zich op dat moment ook bevindt.

## duurzame identifiers geborgd:
* (wereldwijde) unieke identifiers
* procesondersteuning (obv. beleid)
* koppeling externe providers (handle, doi)  
* scope voor duurzame identifiers: objecten, beschrijvingen, termen, versies



