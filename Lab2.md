# Lab 2
####Title:        Writeup for Lab 2 Questions
####Team Members: Jessica Lynch and Noah Dillon


_1. Grammars: Synthetic Examples. 

			A ::= A & A | V
			V ::= a | b

   (a) Rewrite the above grammar using the following two judgment forms:
    
    A &isin; AObjects
    V &isin; VObjects_
    
**	   SOLUTION:**
		
		<in progress>
		


  _(b) Show that the grammar in part (a) is ambiguous:_

**	   SOLUTION:**
    
		Since V => a or b, we can have: 
				A => A & A 
				  => (A & A) & (A & A) 
				  => a & a & a & a 
				   
		However, we can also have:
				A => (A & A) & V 
				  => (V & (A & A)) & V
				  => (a & (V & V)) & a 
				  => (a & (a & a)) & a 
				  => a & a & a & a.
				  
		NOTE: This is only one example of how the grammar in part (a) 
		is ambiguous.  
		
		The above example proves that more than one path can lead us to
		a single result, a & a & a & a. Therefore, the grammar in part
		(a) is ambiguous.

  _(c) Define the language defined by the following grammar:
  
       S ::= A | B | C
       A ::= aA | a
       B ::= bB | &epsilon;
       C ::= cC | c_

**	   SOLUTION:**
    
		L(S) = { a^n | b^m | c^n; n > 1  m >= 1 }
		L(A) = { a^n; n > 1  }
		L(B) = { b^m; m >= 1 }
		L(C) = { c^n; n > 1  }

  _(d) Which of the sentences below are in the language generated by the
       following grammar? (Use derivations.)
  
       S ::= AaBb
       A ::= Ab | b
       B ::= aB | a_

**	   SOLUTION:**
    
		1. baab
		
		   S ::= AaBb => baBb since A => b 
		              => baab since B => a
		   
		   The above derivation shows that baab IS IN the language
		   generated by the above grammar.
	 
	    
	    2. bbbab
	    
	       S ::= AaBb => AbaBb since A => Ab
					  => AbbaBb 
					  => bbbaBb since A => b
					  => bbbaab since B => a
					  
		   The above grammar generates a language that ensures that all 
		   sentences derived from contain more than one 'a' sequentially.
		   Since B => aB or a and S ::= AaBb, the grammar S already 
		   contains a single 'a' followed by grammar B which adds one or
		   more a's to any resulting sentence. 
		   
		        L(S) = { (b)^n(a)^m(b)^k; n >= 1  m > 1  k = 1 }
		        
		   Therefore, bbbab IS NOT IN the language generated by the
		   above grammar.
		
		
		3. bbaaaaa
		
	       S ::= AaBb => AbaBb since A => Ab
					  => bbaBb since A => b
					  => bbaaBb since B => aB
					  => bbaaaBb => (b)^2(a)^5(b)^1 since B => aB or a
		
		   The above grammar generates a language that ensures that all 
		   sentences derived from it terminate in 'b' NOT 'a'. 
		   
		        L(S) = { (b)^n(a)^m(b)^k; n >= 1  m > 1  k = 1 }
		   
		   Therefore, bbaaaaa IS NOT IN the language generated by the
		   above grammar.
		 
		   
		4. bbaab
		
		   S ::= AaBb => AbaBb since A => Ab | b
					  => bbaBb 
					  => bbaab since B => aB | a
		
		   The above derivation shows that baab IS IN the language
		   generated by the above grammar.
		   
  _(e) Which of the below sentences are in the language generated by the
       following grammar? (Use parse trees.)
  
       S ::= aScB | A | b
       A ::= cA | c
       B ::= d | A_

**	   SOLUTION:**
    
		1. abcd
		
				S
			  /| |\
			 a S c B
			   |   |
			   b   d
			    
		   The above parse tree shows that abcd IS IN the language 
		   generated by the above grammar.
		
		2. acccbd
		
				S
			  /| |\
			 a S c B
			   |   |
			   A   d
			  /|
			 c A
			   |
			   c
		   
		   The above parse tree shows the resulting sentence of acccd
		   since b is not in the grammar B or the grammar A, so we can
		   conclude that acccbd cannot be obtained by using the language
		   generated by the above grammar. Therefore, acccbd IS NOT IN 
		   this language.
		   
		3. acccbcc
		
				S
			  /| |\
			 a S c B
			   |   |
			   A   A
			  /|   |\
			 c A   c A
			   |     |
			   c     c

		
		   The above parse tree shows a resulting sentence of accccc 
		   since b is not in grammar B or in grammar A, so we can conclude 
		   that acccbd cannot be obtained by using the language generated 
		   by the above grammar. Therefore, acccbcc IS NOT IN this 
		   language.
		
		4. acd
		
				S
			  /| |\
			 a S c B
			  /|   |
			 A b   d
			 |
			 c
		   
		   The above parse tree shows the resulting sentences as either
		   accd or abcd, so we can conclude that acd IS NOT IN the
		   language generated by the above grammar.
		   
		5. accc
		   
				S
			  /| |\
			 a S c B
			   |   |
			   A   A
			   |   |
			   c   c
			   
		   The above parse tree shows that accc IS IN the language 
		   generated by the above grammar.   
		   
_2. Grammars: Understanding a Language._

  _		 e ::= operand | e operator operand_
  
  _		 e ::= operand esuffix_
  _esuffix ::= operator operand esuffix | &epsilon;_ 

  _(a) Consider the above two grammars for expressions e.  In both grammars, **operator**
	   and **operand** are the same._
	    
**	SOLUTION:**
  
		i. Intuitively describe the expressions generated by the two grammars:
		
		In the former expression e, we have:
		
			L(e) = { (operand)^n(operator operand)^m; n = 1  m >= 1 }
		
		In the latter expression e, we have:
		
			L(e) = { (operand)^n(operator operand)^m; n = 1  m >= 0 }
		
		
		ii. Do these grammars generate the same or different expressions? Explain.
		
		These grammars can generate the same expression where e is as follows:
				
				operand operator operand
				
		However, the latter grammer contains epsilon or empty and therefore
		it's language is slightly different.  Consequently, the resulting
		expression e could differ from that of the former as follows:
		
				operand
		
		Explanation using derivations:
		
			For e ::= operand | e operator operand, we can have:
			
				e => e operator operand
				  => operand operator operand
		
			For e ::= operand esuffix and esuffix ::= operator operand esuffix | epsilon
			where epsilon signifies "Empty", we can have:
			
				e => operand esuffix
				  => operand operator operand esuffix
				  => operand operator operand epsilon
				  => operand operator operand
       

       




