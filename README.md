# **blacklab-demo**

This repository demonstrates how to build Blacklab corpus via Docker and Nginx.

<p align="center">
    <img src="./assest/demo.png" width="100%" height="100%" />
</p>

## **Overview of the Architecture**

```mermaid
flowchart LR
subgraph Internet
    D[Client]
end

subgraph DOCKER [Docker]

  D --> N{"Load Balancer <br/> (Nginx)"}

  N <==> B["/corpus-frontend"]
  N <==> C["/blacklab-server"]


  C <==> I
  B <==> C


  subgraph Indexes
        I[("<div style='padding: 0rem 0.5rem;'>Indexes  <br/>(by Indexer)</div>  ")]
  end


end
```

## **Documentation**

### 1. Installation

Clone the repository and make sure you are in the project directory

```bash
git@github.com:PTT-Corpus/blacklab-demo.git && cd blacklab-demo
```

### 2. Create indexes for Blacklab server

To index your data, you need to add your xml data to the folder `/data` (in `./indexer/data`).

```
deployment\
 |-- ...
indexer\
 |-- formats\                  # custom blacklab index format
 |-- data\
 |   |-- dcard_mock_data.xml   # dcard mock data
 |   |-- ptt_mock_data.xml     # ptt mock data
 |-- ...
server\
 |-- ...
```

We assume here that you are familiar with the BlackLab indexing process; see [indexing with BlackLab](https://inl.github.io/BlackLab/indexing-with-blacklab.html) to learn more.

### 3. Build the server

To build the server for the first time:

```bash
docker compose up
```

Your index should now be accessible at http://localhost/corpus-frontend/.

Once the server builds successfully, a folder `blacklab-indexes` will be generated and used by the blacklab server (i.e. its corresponding Docker container).

Hereafter, if you want let the blacklab server add new indexes, you need to stop the blacklab server by:

```bash
docker compose down
```

Then add your new xml files to the folder `./indexer/data`, and run:

```bash
docker compose up
```

## Contact Me

If you have any suggestion or question, please do not hesitate to email me at philcoke35@gmail.com
