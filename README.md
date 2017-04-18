# bin
- indexes mais acessados.
- io stall
- mapeamento de acesso aos drives
- mapeamento de acesso aos datafiles
- split tempdb
- replica do tempdb
  - storage:  discos do tempdb sao replicados.
              max queue depth
- filegroup arquitetura
- tamanho da reindexação (tempo estimado);
- nao prod
  - como deve ser solicitado essas alterações
  - desafio (volume X representatividade)
  - como medir ambiente atual X ambiente proposto
    -> response time.
- estrategia de rollback
- janela de manutenção.

# oltp workload I/O access patterns
  - frequent writes to data files and log files;
  - some worload in OLTP are volatile ( datafile changes a lot);
  - frequent reads from datafiles if active part of your database does not fit in buffer pool
      - use cluster columnstrore index
      - regular old page
      - row data compression 
      + all these things to try more data in buffer pool
  - writes to a single database log files (log files are sequential);
  
 # dw workload I/O access patterns
   - frequent sequencial read from datafiles
      - use data compression (fit into buffer pool)
      - use cluster columnstrore index
      - little use of log files (except in case of large loads)
      - sequencial reads are very important ( all data does not fit into buffer pool, storage subsystem is very important in this case

# olap workload I/O access patterns
  - frequent random reads from cube files (random IO performance is quite important!FLASHDRIVE!)
  - during build cube files, sequential write performance (think about RAID levels)
  
# layers of I/O optimization;
  - 1 indexing and query tuning
    - workload tuning:
      - find the most expansive SPs and queries
      - focus on top five SPs or queries and prioritize area where instance is under stress
      - make it a team effort and a iterative process (DEV and DBA team), and do this while necessary to get.
    - index tuning:
      - proper index;
      - consider your overall workloads and individual table volatily
      - consider data compression and index columnstore
  - 2 SQL Server instance configuration
  - 3 Operation system configuration (optimization)
  - 4 hardware and storage configuration
