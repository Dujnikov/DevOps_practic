test-ant:  
  stage: 
    test-ant
  only:    
    - feature/2013
  tags:
    - RedOS
  script:
    - ant -d -find ./opt/aeca/ejbca/modules/aeca-plugin-InteractionWrapper/
  when: manual
  allow_failure: true