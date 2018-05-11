.. _near_sync:

--------------
Near Sync
--------------

- NuStuff - <Near Synchronous Replication>
- AOS Version 5.5

Description
+++++++++++

Near-Sync is Replication optimization that allows for up to one minute RPO for Mission-critical Applications.

Pre-requisites
++++++++++++++

- Minimum AOS - Version 5.5
- Licensing AOS - Ultimate Edition
- Supported on X hypervisors - ESX & AHV
- Supported on X hardware platforms - Supported on all platforms except 1&2 Node ROBO

Why are we delivering this feature?
+++++++++++++++++++++++++++++++++++

- This feature has been introduced in order to achieve an RPO > 60 minutes.
- Allows for Minimal data loss during a disaster.
- Provides Granular Restore capabilities.
- Comparable RPO to high end storage arrays.
- Simple to configure, and Restore from.


Example Use Cases
.................

- Primary use case Is for any client who has a need for > 60 min RPO

Reference
.........

- who this functionality was built for
- a quick story, hopefully real

Highlights of case studies
..........................

- “Most recently Peco Pallet joined us in NYC of our TechBootcamp and Beers with engineers event and that continued to close the loop. Unfortunately, our competition would not be derailed, at the bootcamp Peco received incredibly discounted special pricing to keep them with Dell/EMC/VMware with SRM.  At this point we were in a bind as Peco's CIO and CFO were more keen on price then they were on a total solution overhaul. I worked with Peco and Johnny Walker Blue to rebuild an ideal platform for them so they could utilize near-sync replication and get the storage and compute they needed. Finally, after much back and forth we were able to settle on a number and get them to see the light.” Nick Harrison AE

- “This DR expansion of existing Nutanix clusters will give them near-sync capabilities and speed up their data center move initiative. Today their DR runs on IBM servers with EMC VNX storage storage arrays replicated by Avamar & Data Domain. Akron Children's hospital has designated Nutanix as the #1 IT enabler for all that they do to support the children they serve, which means LeBron James, who lives down the street from the hospital, can rest easier at night knowing his kids pediatric care is backed by another world champion-NUTANIX. “  Steve Arroyo AM


How it works
++++++++++++


****************
images here
****************

- Nearsync leverages LWS (Light Weight Snapshots) in order to achieve lower RPO.  The above shows how LWS works, and how it works during replication.
- With Light Weight Snapshots we have continuous data protection like technology. For every Light Weight Snapshot; We use markers into Oplog, instead of creating a new independent vdisk for every snapshot, like we do in Async DR.
- For NearSync every write whether sequential or random goes through Oplog(similar to what we have in Metro).​
- All LWS’s land on SSDs and never on HDDs, we call this the LWS Store.
- LWS Store’s are carved out of an Extent Store residing on SSDs​ LWS get replicated to the remote cluster continuously. This is a departure from earlier Replication which was differential based.
- For restores you can select any minutely LWS available​


Feature History
...............

- High level changelog of the feature over last 2 - 3 major relases
- Context to any re-engineering of the feature (IE change to compression algorithm)

Who is the competition
++++++++++++++++++++++

- For NearSync we are competing with everyone.  This feature is more for parity with other’s than a new concept.  However this is a very critical feature, that has been very heavily asked for.


How we do it better
...................

- For this section I would focus on how it’s the same look and feel / ease of use as our traditional protection domains, with a more aggressive RPO.  The real meat here is we can now do > 60 min RPO, and it’s easy!


Battlecard
..........


Objection Handling
..................

- Obj1
- Obj2
- Obj3

What we are missing today compared to mainstream competition
............................................................

- Missing1
- Missing2
- Missing3

Loose features
..............

- info1
- info2
- info3

How to Demo
+++++++++++

- Provide Flowchart and steps to demo a features
- Provide additional value commentary for relevant next steps

Scenario Setup
..............

- Can you use Demo.nutanix.com to effectively demo this features
- Additional steps required to stage the demo

  - VM Creations
  - Dummy Data
  - Scripts
  - ETC.

  How to POC (If different from How to Demo / Scenario Setup)
  ...........................................................

  - info1
  - info2

  Sizing Considerations
  +++++++++++++++++++++

- Near-Sync replication uses the same process as our normal replication, with the addition that you need to also include the first full copy of the protection domain as well as delta changes based on the schedule.
- For sizing start with 130% of the protection domain plus the required LWS reserve space
- Use drives with the same or greater capacity at the remote site as compared to the drives in the primary cluster to ensure that there is enough LWS reserve space.
- Since de-duplication is not supported on the primary for Near-Sync, make sure your sizing number’s are correct.


  Gotcha's
  ++++++++

- 15 Min RPO is supported only for one remote site. Additional remote sites can still do >1hr RPO
- Minimum RPO for replication to Storage Heavy cluster stays one hour
- Minimum RPO for replication to Storage Heavy cluster stays one hour
- Self Service Restore will only work on full snapshots
- Near-sync does not currently honor maximum bandwidth thresholds
- Nutanix offers near-sync with a telescopic schedule (time-based retention). When you set the RPO to be ≤15 minutes and ≥ one minute, you have the option to save your snapshots for X number of weeks or months.
- Once you select near-sync, you cannot add any more schedules
- Linked clone VM’s (typically non-persistent View desktops) are not supported.
- Metro and SRM-protected containers are not supported
- Don’t configure near-sync for Hyper-V
- Ensure that you have enough bandwidth to support the change rate
- Deduplication on the source container is not supported.
- Minimum 1.2 TB SSD are needed in hybrid systems.
- Third party out of band snapshots are not allowed when Near-Sync is in use.
- Limit the number of VM’s to 10 or fewer per protection domain.
- If possible maintaining one VM per protection domain can help you transition back from Near-Sync, if you run out of LWS reserve storage


  FAQ
  +++

  - FAQ1
  - FAQ2
  - FAQ3

  Links
  +++++

  - NearSync Debugging Techniques	http://wikid.nutanix.com/wiki/Debugging_Near_Sync​​
  - JIRA : FEAT-911​​
  - Test Plan and Automation https://nutest-grok.eng.nutanix.com/source/xref/nutest/testcases/systest/nearsync/ (System tests)​
  		  https://nutest-grok.eng.nutanix.com/source/xref/nutest/testcases/near_sync/ (Functional + Long running)​
  - NearSync Design Docs​ https://sites.google.com/a/nutanix.com/corp/eng-wiki-gen-2/cerebro/near-sync
