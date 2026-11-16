RPKI DOCTORS CHECKLIST 
============================

1. Is there explicit guidance as to which fields are signed with what?

2. Is a 100% deterministic canonical form defined for the eContent? (malleability and variances should be avoided)

3. Is there explicit guidance on the filenaming scheme to prevent race conditions? In general it is best to mandate the use of high-entropy fixed-length short filenames.

4. Is there explicit guidance on whether the signed objects are published in global RPKI repositories or not? In general, detached signatures usually should be avoided because they can lead to inefficiency and non-discoverability. (i.e., detached sigantures are useful when private business is an explicit objective).

5. There should not be any cross-certification/multi-signer for end-entity certificates. This is because signers can never make any assumptions about the contents of the RP's trust store, and a large portion of RPKI participants cannot participate in multi-signer schemes because, for example, they have IP resources in one RIR and AS in another RIR.

6. Is BER avoided? We just got rid of BER in the global RPKI... need to keep an eye on not accidentally reintroducing it!

7. Is some form of 'packing' facilitated (e.g., a single ROA can contain multiple prefixes, this way fewer signatures are needed in turn improving scalability). Designers of new signed objects should contemplate if there is opportunity for some form of aggregation.

8. Are ASN.1 SETs avoided in eContent? Instead of ASN.1 SETs everyone should always use SEQUENCE for improved interoperability and deterministic outcomes.

9. Is the draft under review actually adhering to the CMS Signed Object template? (e.g., could be some author somewhere thinks CMS is too bothersome and proposes to reference raw bytes blobs from Manifests. However, every object on a Manifest _must_ be a CMS signed object, a certificate, or a CRL. The RPKI specifications don't permit non-CMS/non-CER/non-CRL data types.

10. Are there actual implementations? There have been a few instances where draft authors entirely misfired in how to make the best use of the RPKI in part due to lack of any implementation experience. RPKI Doctors should ask for implementation reports, test vectors, and a multi-vendor interoperability story. Even if a WG does not require implementations we should be adament that the RPKI is too important to apply a 'yolo' strategy and avoid implementation-before-publication.