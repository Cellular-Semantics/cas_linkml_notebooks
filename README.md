# BG taxonomy hacking experimental_notebooks 

Aims: 

- [x] Check CL term curation up to date

* Test flattening human BG tax + h5ad - for CAP
   Notes:
     1. It seems that everything is flattened. We should review this, it conflicts with option 2 here:
        https://github.com/cellannotation/cas-tools/issues/111
          Decision - we will stick with the status quo for now, but need to review.  The flattened files are ugly, but we can offer unflattening.
          TODO - check what happens when we flatten annotation transfer.
     3. We are getting some warnings about hashes.
     4. TDT issue:
         * Hierarchy merges down where two adjacent levels have the same name.  Needs to be fixed. <-- v.high priority.
   Action item: Fix TDT issue and then share flattened human BG taxonomy with CAP.
   Action term: Review roundtripping - should we switch to mixed strategy?
  

* Add cell set level AT to Macaque BG tax
   *  Agree on solution. Draft:
      * AT was on clusters, so they all get the most specific (homology subclass)
      * Everything else gets most specific matching block - if one exists
      * e.g. for
      *  <img width="993" alt="image" src="https://github.com/user-attachments/assets/4f0c0462-d4af-4c2c-a839-381d66f88b30">
        * primate subclass:
          * CCK-FBXL7: CTX-MGE GABA
          * CCK-VIP-TAC3:vip Gaba
          * CHAT:PAL-STR Gaba-Chol
          * D1-ICj:OT D3 Folh1 Gaba
      * primate-neighbourhood:
          * Astroyctes: Astro-Epen
          * CCK:CTX-MGE GABA
          * TAC3:CTX-CGE GABA
          * cholinergic: PAL-STR Gaba-Chol
       
  If there are mutiple matches on the same level, we add all, again matching most specfic block

  <img width="816" alt="image" src="https://github.com/user-attachments/assets/06c0ca33-0ec4-491a-a2cb-791725c80308">

  41_In :  287 + 288
  
  CCK-FBKXL7 : 287 + 288
  
  etc

  Consider adding a gropuing mechanism in future
       
   * Current schema:
     - **`transferred_annotations`** *(list)*
        - **`transferred_cell_label`** *(string)*: Transferred cell label.
        - **`source_taxonomy`** *(string)*: PURL of source taxonomy.
        - **`source_node_accession`** *(string)*: accession of node that label was transferred from.
        - **`algorithm_name`** *(string)*: .
        - **`comment`** *(string)*: Free text comment on annotation transfer.
      
      - Notes - we need a new field for labelset
      - We need confirmation of algorithm and some text for the coment from Nelson
        
   * Code with new CAS-LinkML lib.
      * LinkML misfeature means that author annotation fields get stored as JSON_to_string which is a not a JSON string.  Solution for now - we convert to JSON string before loading into CAS-LinkML instance.  Convert back at end.
 
* (Test) Merge Macaque BG tax with new h5ad
