# Target Explorer Docs

## Documentation for the [AMP PD Target Explorer Tool](https://target-explorer.amp-pd.org/)

These documents are intended to help you familiarize yourself with the features of the AMP PD Target Explorer.
You will find explanations of how to use the AMP PD Target Explorer website to explore and discover the latest research around your favorite biomarkers.
You will also find examples for how to retrieve data via the [Target Explorer API](https://api.target-explorer.amp-pd.org/docs).

Thank you for interest! We would love to hear your thoughts and feedback. Please use the feedback form on the 
[Target Explorer homepage](https://target-explorer.amp-pd.org/), 
or file a GitHub issue here to let us know if you have a specific problem with using the Target Explorer website or the
[Target Explorer API](https://api.target-explorer.amp-pd.org/docs).

## FAQs
- What can I do with the Target Explorer?
    - The Target Explorer provides tools for exploring genes that have been nominated by the research community as potential biomarkers associated with Parkinson’s Disease.
    You can explore the list of all nominated targets, or search for specific genes, transcripts or proteins. 
    You can discover if your favorite genes/transcripts/proteins have been nominated by other researchers, and learn more about their research.
- Where do the Target Lists come from?
    - Target Lists are contributed by researchers eager to share their work with the community. The AMP PD program also funds research into identifying PD biomarkers.
- What is AMP PD?
    - AMP PD stands for Accelerating Medicines Partnership - Parkinson’s Disease. Please visit the [AMP PD website](www.amp-pd.org) for more information.
- How can I contribute my Target List?
    - Fantastic! Please fill out our [Become a Contributor](https://target-explorer.amp-pd.org/become-a-submitter) form.

## Features

### View Teams and Target Lists

- View Information About Contributing Teams
    - You can view information about the teams that contributed Target Lists by clicking on the [Teams & Lists](https://target-explorer.amp-pd.org/teams) link at the top of the website.

- View Target Lists Contributed by Each Team
    - Each Team section on the “Teams & Lists” page contains links to List Details pages with further details for each Target List contributed by that team.
        - Analysis Methodology describes the processes used to produce the Target List.
        - Analysis Data contains the data fields produced from the research that supports nomination of each target. 
        - Analysis Links will take you to external sites such as Terra or Github or others. Contributors may provide these links for example source code or more detailed information about their work.

### Search For Specific Genes, Transcripts, Proteins
- Type in a gene or UniProt ID in the Search bar from the [Home](https://target-explorer.amp-pd.org/) page or the [Target Search](https://target-explorer.amp-pd.org/genes/target-search) page, then select from the auto-complete suggestions. You must select one of the auto-complete suggestions for it to be added as a search term.
    Input symbols can be HGNC symbols, Ensembl IDs, or UniProt IDs.
    The selected symbol is added to the Custom Input box. You can think of the Custom Input box as a “shopping cart” that contains all the unique search terms you have selected. Genes from selected Target Lists and Pathways are not shown in the Custom Input box.
- Paste a list of symbols into the Custom Input box.
    You can paste a list of symbols into the Custom Input box. The list can be delimited with commas, spaces, tabs and newlines.
    You can also manually edit symbols in the Custom Input box.
    Input symbols must match exactly a symbol known to the system (case insensitive).

### More Information on Searched Symbols
- Your input symbols will sometimes return no search results. This could be due to several reasons including misspelled symbols, symbols unknown to the system, and the gene/transcript/protein was not nominated in any Target Lists in the system.
- Click the “More Info” button under the Custom Input box to show more detailed information about why each searched symbol returned results, or why there were no results found.

### Select Genes, Transcripts, Proteins From Target Lists and Pathways
- Select single or multiple Target Lists to show all the genes/transcripts/proteins that were nominated in those Target Lists.
- Select single or multiple Pathways to search for nominated genes from those Pathways
    - For example, the Pathway named “Fatty acid biosynthesis - Homo sapiens (human)” comprises 18 genes. By selecting that Pathway, we see in the search results table that the gene “OLAH” from that Pathway was nominated in the Target List named “AMP PD Transcriptomics Differential Expression All Time Points”.

### Download Target Lists and Search Results
- Download individual Target Lists and Metadata docs
    - The List Details pages provide Download buttons that will initiate a download package for that list. The package contains:
        - A CSV file containing the analysis data fields.
        - A PDF document containing information about the team and the analysis behind the Target List.
- Download Search Results table and all Target Lists found in results
    - The Target Search page provides a Download button that will initiate a download package for the search results. The package contains:
        - A CSV file containing information about the search symbols and the Target Lists they were found in.
        - For each Target List that contains a search symbol, you will get the same files as if you had downloaded the Target List separately.


## Target Explorer API

### What are OpenAPI, Swagger and FastAPI?
- [OpenAPI](www.openapis.org) is a specification for defining <i>Application Programming Interfaces</i> (APIs) that are understandable to others.
- [Swagger](https://swagger.io) is a set of tools to help developers implement the OpenAPI specification.
- [FastAPI](https://fastapi.tiangolo.com/) is a framework for building production-quality APIs based on open standards, e.g. OpenAPI and [JSON Schema](https://json-schema.org/)
- The [Target Explorer API](https://api.target-explorer.amp-pd.org) uses the FastAPI web framework and Swagger to auto-generate interactive API documentation..

### Services
- The [Target Explorer API](https://api.target-explorer.amp-pd.org/docs) provides REST service endpoints used by the application to retrieve data and interact with the database.
- These endpoints can be used directly in a terminal with curl, or in a browser with a url query.
- The [Postman](https://www.postman.com/) application can also be used to easily build and save queries for reuse.

### Queries
- The [Target Explorer API docs](https://api.target-explorer.amp-pd.org/docs) page provides information on parameters and schemas for some of our public endpoints.
- There is a [/general-query](https://api.target-explorer.amp-pd.org/docs#/default/general_query_general_query__get) endpoint that allows users to construct any "find" query they wish, using the MongoDB Query Language (MQL) syntax.  Again, queries are limited to “find” requests. Please see the documentation for the [MongoDB find](https://www.mongodb.com/docs/manual/reference/method/db.collection.find/) method.
- Here is an example for finding the first 10 entries in our database of symbols that have a known alias. The collection is named "gtpinfo", and the query field is named "alias_symbol".

Example query:

    {
        "collection": "gtpinfo",
        "query": {"alias_symbol": {"$ne":null}},
        "projection": {"_id": 0, "hgnc_symbol": 1, "ensembl_gene_id": 1, "alias_symbol": 1},
        "limit":10
    }

- Here is an example for finding the names of target lists that are unpublished.. The collection is named "targetlists", and the query field is named "publication_status".

Example query:

    {
        "collection": "targetlists",
        "query": {"publication_status": "Unpublished"},
        "projection": {"_id": 0, "name": 1},
    }

- Feel free to contact us for help with constructing any queries that would be useful to you! :smiley:
> [!NOTE]
> Limits: Please limit your queries to no more than 1 per second to avoid disruptions for other users. Bulk data downloads are most easily performed from the [Teams](https://target-explorer.amp-pd.org/teams) page or the [Target Search](https://target-explorer.amp-pd.org/genes/target-search) page.
