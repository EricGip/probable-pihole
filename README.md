Introduction
______

   * My housemates and I come from different backgrounds but the one thing we connect on is our Chinese heritage and our love for consumer technology. We all love the idea of the smart home and thus all have an amazon Echo or Google Home. 
   * One day, they both watched a LinusTechTips video and was inspired to get a smart outlet to further automate their rooms. 
   * It took us a while, but we noticed that our WiFi and home network was significantly slowed down. Normally it would take less a minute to  download a 1 gb file with our current plan, but it was now taking up to 15 - 20 minutes to download the same file. 
    * From AWS Lambda, the web service that powers Alexa skills, I understood how difficult it was to set up a system that doesn't have to constantly send queries and hoping for an input. THis was just a theory and I had to find a way to quantify the hypothesis.
   * After some research and my current Raspberry Pi infrastructure, I decided to docker pull Pi - Hole to gather the data.
    * First, I downloaded an IP scanner (angry IP scanner is wonderful) and utilized SSH to configure the admin account for Pi-Hole and be able to access the dashboard. Then, we had to route our router DNS to go through the Raspberry Pi and we were done. This quick installation was only possible due to the insane amount of time I spent trying to configure Kubernetes and Docker, which is another post on its own. 
      * insert picture here and dashboard stuff

        * Note: This is a reverse DNS, as told by the .arpa and literally our DNS backwards. It's communicating to every device connected to our router. From my IT risk analyst position, I was kind of wary about this dvice.

Potential Solutions: 
Top of the head brute force solution:
    * Use Pi-hole dashboard to block all device reverse DNS queries to the devices connected to our router that we don't want it communicating to. 

    * The problem with this solution is that this IoT device can still pose as a security risk. In essense, if the IoT software was this poorly optimized and cheap ($10), it would not be wise to trust the manufacturer to account for the vulnerabilities that come with the early age of IoT.
        * Note: I tried this solution because I was curious of the results. Just blocking the queries alone would still be using data and accounted for over 10% of our monthly plan at the current rate.      
        * Ultimately, he decided to just return the device and do more research on his next smart home purchase.

Conclusion
-------
After seeing this information on our top queries, it seems like the smart outlet was sending a query each minute to request a reverse DNS look up, essentially sending an unintentional Distributed Denial of Service attack on our network and throttling the system. 

I am proud of this project because I was able to use my various interests and background to solve a real world problem:
   * AWS certificate that exposed me to IoT & webservices to hypothesize that the smart outlet should be investigated.  
   * Statistics and Data Science to understand to gather quantifiable data.  
   * Practice DevOps by my RPi kubernetes - docker cluster I spent a long time setting up, the infrastructure allowed for a really simple installation.  
   * Used security experience gained from my IT Risk Anaylst position and frameworks that exposed me to various vulnerabilities & attacks, mainly Cloud and IoT vulnerabiities. 
