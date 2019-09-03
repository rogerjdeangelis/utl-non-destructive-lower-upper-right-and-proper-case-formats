# utl-non-destructive-lower-upper-right-and-proper-case-formats
Non-destructive lower, upper, right, and proper case formats

    Non-destructive lower, upper, right, and proper case formats                                                 
                                                                                                                 
    github                                                                                                       
    https://tinyurl.com/y4qn4yud                                                                                 
    https://github.com/rogerjdeangelis/utl-non-destructive-lower-upper-right-and-proper-case-formats             
                                                                                                                 
    *_                   _                                                                                       
    (_)_ __  _ __  _   _| |_                                                                                     
    | | '_ \| '_ \| | | | __|                                                                                    
    | | | | | |_) | |_| | |_                                                                                     
    |_|_| |_| .__/ \__,_|\__|                                                                                    
            |_|                                                                                                  
    ;                                                                                                            
                                                                                                                 
    data have;                                                                                                   
                                                                                                                 
      length name $32;                                                                                           
                                                                                                                 
      set sashelp.class(obs=4);                                                                                  
                                                                                                                 
       name=catx(" ",lowcase(name),substr(name,2,1),"SMITH");                                                    
       keep nam: age;                                                                                            
                                                                                                                 
    run;quit;                                                                                                    
                                                                                                                 
    WORK.HAVE total obs=4                                                                                        
                                                                                                                 
           NAME          AGE                                                                                     
                                                                                                                 
      alfred l SMITH      14                                                                                     
      alice l SMITH       13                                                                                     
      barbara a SMITH     13                                                                                     
      carol a SMITH       14                                                                                     
                                                                                                                 
    *            _               _                                                                               
      ___  _   _| |_ _ __  _   _| |_                                                                             
     / _ \| | | | __| '_ \| | | | __|                                                                            
    | (_) | |_| | |_| |_) | |_| | |_                                                                             
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                            
                    |_|                                                                                          
    ;                                                                                                            
                                                                                                                 
      NAME                        AGE                                                                            
                                                                                                                 
      Alfred L Smith               14                                                                            
      Alice L Smith                13                                                                            
      Barbara A Smith              13                                                                            
      Carol A Smith                14                                                                            
                                                                                                                 
    *                                                                                                            
     _ __  _ __ ___   ___ ___  ___ ___                                                                           
    | '_ \| '__/ _ \ / __/ _ \/ __/ __|                                                                          
    | |_) | | | (_) | (_|  __/\__ \__ \                                                                          
    | .__/|_|  \___/ \___\___||___/___/                                                                          
    |_|                                                                                                          
    ;                                                                                                            
                                                                                                                 
    options cmplib=(work.functions);                                                                             
    * functions in formats Rick Langston;                                                                        
                                                                                                                 
    proc fcmp outlib=work.functions.chrfun;                                                                      
      function pcase(txt $) $32;                                                                                 
        prp=propcase(txt);                                                                                       
      return(prp);                                                                                               
      endsub;                                                                                                    
      function lcase(txt $) $32;                                                                                 
        prp=lcase(txt);                                                                                          
        return(prp);                                                                                             
      endsub;                                                                                                    
      function ucase(txt $) $32;                                                                                 
        prp=upcase(txt);                                                                                         
        return(prp);                                                                                             
      endsub;                                                                                                    
      function charRight(txt $) $32;                                                                             
        ryght=right(txt);                                                                                        
        return(ryght);                                                                                           
      endsub;                                                                                                    
    run;quit;                                                                                                    
                                                                                                                 
    * put the function in a format;                                                                              
    proc format;                                                                                                 
      value $pcase other=[pcase()];                                                                              
      value $ucase other=[ucase()];                                                                              
      value $lcase other=[lcase()];                                                                              
      value $charRight other=[charRight()];                                                                      
    run;quit;                                                                                                    
                                                                                                                 
    proc print data=have;                                                                                        
    format _character_ $pcase24.;                                                                                
    run;quit;                                                                                                    
                                                                                                                 
