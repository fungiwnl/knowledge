# Global Accelerator

- You have deployed an application and have global users who want to access it directly.
- They go over the public internet, which can add a lot of latency due to many hops 
- We wish to go as fast as possible through AWS network to minimize latency

## Unicast IP vs Anycast IP

- Unicast IP: one server holds on IP address
- Anycast IP: all servers hold the same IP address and client is routed to the nearest one

- Leverage the AWS internal network to route to your app
- 2 Anycast IP created for your app
- The Anycast IP send traffic directly to Edge Locations
- The Edge locations send the traffic to your app

## Compatibility

- Works with Elastic IP, EC2, ALB, NLB, public or private
- Consitenct performance
- Health checks
- Security

## Global Accelerator vs Cloudfront

- Cloudfront
  - Improves performance for cacheable content like images and videos
  - Dynamic content
  - Content is served at the edge

- Global Accelerator
  - Improves performance for a wide range of apps over TCP or UDP
  - Proxying packets at the ege of apps running in one or more AWS regions
  - Good fit for non HTTP use cases such as gaming (UDP), IoT (MQTT) or Voice over IP
  - Good for HTTP use cases that require static IP
  - Good for HTTP use cases that required deterministic, fast regional failover

## Practical

- Create EC2 instance (t2.micro)
- User data 
- HTTP security group from anywhere (0.0.0.0)
- Navigate to another region e.g. Sydney for same process
- Create accelerator (listener: 80 ports, TCP, None client affinity)
