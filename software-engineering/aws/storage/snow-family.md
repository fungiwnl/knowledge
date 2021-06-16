# AWS Snow Family 

- Highly secure, portable devices to **collect and process data at the edge** and **migrate data into and out of AWS**

- Data migration:
     - Snowcone
     - Snowball Edge
     - Snowmobile

- Edge computing:
     - Snowcone
     - Snowball Edge


## Data Migrations

- It takes a lot of time to trasnfer 
- Challenges include:
    - Limited connectivity
    - Limited bandwidth
    - High network cost
    - Shared bandwidth (can't maximize the line)
    - Connection stability

- If it takes more than a week to transfer over the network, use Snowball devices 

### AWS Snowball Edge (for data transfers)

- Physical data transport solution: move TBs or PBs of data in or out of AWS
- Alternative to moving data over the network (and paying network fees)
- Pay per data transfer job
- Provide block storage and Amazon S3-compatible object storage

- Snowball Edge Storage Optimized
    - 80 TB of HDD capacity
- Snowball Edge Compute Optimized
    - 42 TB of HDD capacity 

### AWS Snowcone

- Small, portable computing, anywhere, rugged & secure, withstands harsh environments
- Light (4.5 pounds, 2.1kg)
- Device used for edge computing, storage and data trasnfer
- 8 TBs of usable storage
- Use Snowcone where Snowball does not fit (space-constrained environments)
- Must provide your own battery / cables

- Can be sent back to AWS offline, or connect it to the internet and use **AWS DataSync** to send data

### AWS Snowmobile

- Transfer exabytes of data (1 EB = 1,000 PB = 1,000,000 TBs)
- Each Snowmobile has 100 PB of capacity (use multiple in parallel)
- High security: temperature controlled, GPS, 24/7 video surveillance
- Better than Snowball if you transfer more than 10 PB


## Edge Computing

- Process data while it's being created on an edge location
   - A truck on the road, a ship on the sea, a mining station underground

- These locations may have
   - Limited / no internet access
   - Limited / no easy accces to computing power

- We setup a Snowball Edge / Snowcone device to do edge computing

- Uses cases of Edge computing:
   - Preprocess data
   - Machine learning at the edge
   - Transcoding media streams

- Eventually, you can ship back the device to AWS (for trasnferring data for example)

### Snowcone

- 2 CPUs, 4 GB of memory, wired or wireless access
- USB-C power using a cord or the optional battery

### Snwoball Edge (Compute Optimized)

- 52 vCPUs, 208GiB of RAM
- Optional GPU (Useful for video processing or ML)
- 42 TB usable storage

### Snowball Edge (Storage Optimized)

- Up to 40 vCPUs, 80GiB of RAM
- Object storage clustering available 

- They all can run EC2 instances & AWS Lambda (using AWS IoT Greengrass)
- Long term deployment options: 1 and 3 years discounted pricing 

### AWS OpsHubs

- Historically to use Snow Family devices, you needed a CLI
- Today you can use AWS OpsHubs (software to install on your computer) to manage your Snow Family Device
    - Unlocking and configuring single or clustered devices
    - Transferring files
    - Launching and managing instances running on Snow Family Devices
    - Monitor device metrics (storage capacity, active instances on your device)
    - Launch compatible AWS services on your services (ex: Amazon EC2 instances, AWS DataSync, Network File System (NFS))