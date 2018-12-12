Taylor's Final Project README

This is a script for a variant classification system, which looks at a specific length of DNA transcript. The user inputs the transcript, at which point the program will ask if the the user would like to randomly mutate it. Once the user inputs a yes/no response, the system will randomly mutate one base and determine the amino acid sequence, when it will then prompt the user to determine if the sequence of amino acids was changed. If it was, the system will spit out a response that says it is "potentially pathogenic" and if the user inputs that it did not change the sequence, it will say that the mutation was a "silent mutation, likely benign."

This script was created using Python 3.7. The user will need a DNA transcript to input.

Installation Instructions:

'''python
#DNA input screen
DNASeq = "ATGAACCTAGACATAAAGATGCATGCATCGATC"
DNASeq = input("Enter a DNA sequence: ")
DNASeq = DNASeq.upper()
DNASeq = DNASeq.replace(" ","")

print ('Sequence:', DNASeq)

#define sequence to amino acid, create table to define off of
def translate(seq): #defines what translate(seq) means, following creates a table of amino acids
	
	table = { 
		'ATA':'I', 'ATC':'I', 'ATT':'I', 'ATG':'M', 
		'ACA':'T', 'ACC':'T', 'ACG':'T', 'ACT':'T', 
		'AAC':'N', 'AAT':'N', 'AAA':'K', 'AAG':'K', 
		'AGC':'S', 'AGT':'S', 'AGA':'R', 'AGG':'R',				 
		'CTA':'L', 'CTC':'L', 'CTG':'L', 'CTT':'L', 
		'CCA':'P', 'CCC':'P', 'CCG':'P', 'CCT':'P', 
		'CAC':'H', 'CAT':'H', 'CAA':'Q', 'CAG':'Q', 
		'CGA':'R', 'CGC':'R', 'CGG':'R', 'CGT':'R', 
		'GTA':'V', 'GTC':'V', 'GTG':'V', 'GTT':'V', 
		'GCA':'A', 'GCC':'A', 'GCG':'A', 'GCT':'A', 
		'GAC':'D', 'GAT':'D', 'GAA':'E', 'GAG':'E', 
		'GGA':'G', 'GGC':'G', 'GGG':'G', 'GGT':'G', 
		'TCA':'S', 'TCC':'S', 'TCG':'S', 'TCT':'S', 
		'TTC':'F', 'TTT':'F', 'TTA':'L', 'TTG':'L', 
		'TAC':'Y', 'TAT':'Y', 'TAA':'_', 'TAG':'_', 
		'TGC':'C', 'TGT':'C', 'TGA':'_', 'TGG':'W', 
	} 
	protein ="" 
	if len(seq)%3 == 0: #determines how to return which amino acid
		for i in range(0, len(seq), 3): 
			codon = seq[i:i + 3] 
			protein+= table[codon] 
	return protein #prompts system to return protein


print ('Amino Acid Sequence:', translate(DNASeq)) #instructs system to print the sequence

#Choice Loop - this will be what the loop further down is defined based on
bad_words = 0
words = ""
wait = 0
choices = ["A",
           "T",
           "C",
           "G",
           ]


import random
import string
orig= DNASeq

char1=random.choice(choices)  #random character1

ran_pos1 = random.randint(0,len(orig)-1)  #random index1

orig_list = list(orig)
orig_list[ran_pos1]=char1
modDNA = ''.join(orig_list)
   
def rtd(): #this will be what the system prints while it is working
    print("Working...")
    time.sleep(2) #spins for 2 seconds
    return("\n" + (modDNA) + "\n")
def modpro():
    return("\n" + (translate(modDNA)) + "\n")
    
    
while True: #creates a loop to ask prompts and use user input to further the sequence.
    if (bad_words != 1):
        print("Do you want to randomly mutate this sequence? Or type 'stop' to close the program.")
    words = input(":")
    if (words == ""):
        bad_words = 1
        print("Please answer yes or no.")
    else:
        bad_words = 0
        if (str.lower(words) == "stop"):
            print("Goodbye")
            break
        print("\n" + rtd() + modpro() + "\n")
        break

print("Did this change amino acid sequence? yes or no") #uses user input
words = input(":")
if (words == "yes"):
    bad_words = 1
    print ("Please answer yes or no.")
    print("\n" + "mutation potentially pathogenic" + "\n")  
if (words == "no"):
    bad_words = 1
    print ("Please answer yes or no.")
    print("\n" + "silent mutation, likely benign" + "\n")
else:
    bad_words = 0
    if (str.lower(words) == "stop"):
        print("Goodbye")