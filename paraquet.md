

paraquet





<img width="427" height="281" alt="image" src="https://github.com/user-attachments/assets/bd242d5e-976d-4098-84c7-5e10e2e6e45e" />

<img width="310" height="322" alt="image" src="https://github.com/user-attachments/assets/148dedce-2a8b-4c4d-bde6-11f5ae6b2b4f" />


Apache Parquet is an open-source, binary file format designed for the efficient storage and retrieval of large datasets. It is a "columnar" format, meaning it stores data by column rather than by row, which makes it the industry standard for analytical (OLAP) workloads in 2026. 
1. Core Structural Logic
Unlike a CSV which stores a full record together (e.g., Name, Age, City), Parquet stores all "Names" together, then all "Ages" together. 
Row Groups: A Parquet file is horizontally partitioned into "Row Groups" (typically 512 MB to 1 GB in size). Each group contains all columns for a specific set of rows.
Column Chunks: Within each row group, data is stored in "Column Chunks"—one for every column in the dataset.
Data Pages: Chunks are further split into "Pages," the smallest unit of storage, which contain the actual encoded and compressed data. 
2. Why It Is Efficient
Column Pruning: If a query only needs 2 columns out of 1,000, Parquet reads only those specific columns from disk, skipping the rest. This drastically reduces I/O.
Predicate Pushdown: Parquet files store metadata (min/max values) for each row group. Query engines use this to skip entire blocks of data that don't match a filter (e.g., skipping a row group where the Age range is 10–20 if you are looking for Age > 30).
Advanced Encoding: Since values in a column are the same type, they compress better. Parquet uses techniques like:
Dictionary Encoding: Replaces long strings with short integer IDs.
Run-Length Encoding (RLE): Stores repeated values (e.g., "USA" appearing 1,000 times) as a single value and a count.
Bit-Packing: Packs small integers into the minimum number of bits required. 
3. Key Advantages
Storage Savings: Typically achieves 60%–75% size reduction compared to uncompressed CSVs.
Self-Describing: The file includes its own schema and metadata, so you don't need a separate definition file to read it.
Complex Data Support: Natively handles nested structures like lists, maps, and JSON-like objects.
Schema Evolution: Allows adding new columns or merging different compatible schemas over time without rewriting old data. 
4. When to Use It
Best for: Large-scale analytics, data lakes (AWS S3, Azure Data Lake), and big data frameworks like Apache Spark, Snowflake, or Trino.
Avoid for: Real-time data updates or simple "human-readable" needs (use CSV or JSON for small, frequently edited files). 




