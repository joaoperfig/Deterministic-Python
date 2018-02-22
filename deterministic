import sys

def reverse(stri):
    return stri[::-1] 
def getname(declaration):
    i = declaration.index("def")
    found = False
    name = ""
    for c in declaration[i+4:]:
        if c in " (":
            if found:
                return name
        else:
            found = True
            name = name + c
def getparams(declaration):
    start = declaration.index("(")
    end = declaration.index(")")
    return declaration[start:end+1]
        

dest = sys.argv[1]
f = open(dest, "r")
text = f.read()
f.close()

#text = "deterministic fib(n):\n    if n <=1:\n         return 1\n    return fib(n-1) + bib(n-2)\n"

if ("\t" in text):
    print("A tab was found on character " +str(text.index("\t"))+", please use only spaces for indentation.")

text = "import random\n\n"+text
while ("deterministic" in text):
    startindex = text.index("deterministic")
    text = text[:startindex] + "def" + text[startindex+len("deterministic"):] # replace "deterministic" with "def"
    try:
        idepth = reverse(text[:startindex]).index("\n") #depth of indentation of function
    except:
        idepth = 0 #function defined on first line
    endindex = 1+startindex+text[startindex:].index("\n") #index of end of declaration line
    beforedecl = text[:startindex-idepth] #text before declaration line
    decl = text[startindex-idepth:endindex] #declaration line
    afterdecl = text[endindex:] #text after declaration line
    
    name = getname(decl) #name of function
    print("Making function "+name+" deterministic...")
    params = getparams(decl) #function parameters
    
    replacement = [] #lines that will replace declaration line (no indentation spaces or \ns)
    
    replacement = replacement + [""] #empty line for good luck
    
    replacement = replacement + ["determ_first_"+name+" = {}"] #declaration of return dics
    replacement = replacement + ["determ_last_"+name+" = {}"] #declaration of return dics
    replacement = replacement + ["def "+name+params+":"] #function delcaration
    replacement = replacement + ["    " +"global determ_first_"+name] #getting global dics
    replacement = replacement + ["    " +"global determ_last_"+name] #getting global dics
    #algorithm stuff
    replacement = replacement + ["    " +"if "+params+" in list(determ_first_"+name+"):"] 
    replacement = replacement + ["    " + "    " + "return determ_first_"+name+"["+params+"]"] 
    replacement = replacement + ["    " +"if "+params+" in list(determ_last_"+name+"):"] 
    replacement = replacement + ["    " + "    " + "return determ_last_"+name+"["+params+"]"] 
    replacement = replacement + ["    " + "determ_res_ult = determ_new_"+name+params] 
    replacement = replacement + ["    " + "if (len(list(determ_first_"+name+")) < 1000):"] 
    replacement = replacement + ["    " + "    " + "determ_first_"+name+"["+params+"]=determ_res_ult"] 
    replacement = replacement + ["    " + "if (len(list(determ_last_"+name+")) > 2000):"] 
    replacement = replacement + ["    " + "    " + "determ_last_"+name+".pop(random.choice(list(determ_last_"+name+")))"]
    replacement = replacement + ["    " + "determ_last_"+name+"["+params+"]=determ_res_ult"]
    replacement = replacement + ["    " + "return determ_res_ult"]
    
    replacement = replacement + [""]
    replacement = replacement + ["def determ_new_"+name+params+":"] #replacement to old declaration that will hold original code
    
    rept = ""
    for line in replacement:
        rept = rept + " "*idepth + line + "\n"
    
    text = beforedecl + rept + afterdecl
    
open("runtime_determinism", "w").close()
f = open("runtime_determinism", "w")
f.write(text)
f.close()
import os
print("Running code...\n")
os.system("python runtime_determinism")
    