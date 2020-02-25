#START
#-  -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   
import re, string, unicodedata
import math


s1 = open('Document_1.txt','r')                 #reading the files where corpus has been saved
s2 = open('Document_2.txt','r')
s3 = open('Document_3.txt','r')

document_list = {s1,s2,s3}                      #list of files

#-  -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -

def normalize_the_document(raw_data):           #normalizing the documents using regular expressions
    
    raw_data = raw_data.lower()
    raw_data = re.sub(r'\[.*\]', '', raw_data)
    raw_data = re.sub(r'\(.*\)', '', raw_data)
    raw_data = re.sub(r'\s+', ' ', raw_data)
    raw_data = re.sub(r'\[[0-9]*\]', ' ', raw_data)
    raw_data = re.sub('[^a-zA-Z]', ' ', raw_data)
    raw_data = re.sub('['+string.punctuation+']', '', raw_data).split()

    return(raw_data)

def stopwords_removal(data):                    #removing the stopwords

    text = []
    
    stop_words = {"a","about","above","after","again","against","ain","all","am","an","and","any","are","aren","aren't","as","at","be","because","been","before","being","below","between",
                  "both","but","by","can","couldn","couldn't","d","did","didn","didn't","do","does","doesn","doesn't","doing","don","don't","down","during","each","few","for","from",
                  "further","had","hadn","hadn't","has","hasn","hasn't","have","haven","haven't","having","he","her","here","hers","herself","him","himself","his","how","i","if","in",
                  "into","is","isn","isn't","it","it's","its","itself","just","ll","m","ma","me","mightn","mightn't","more","most","mustn","mustn't","my","myself","needn","needn't","no",
                  "nor","not","now","o","of","off","on","once","only","or","other","our","ours","ourselves","out","over","own","re","s","same","shan","shan't","she","she's","should",
                  "should've","shouldn","shouldn't","so","some","such","t","than","that","that'll","the","their","theirs","them","themselves","then","there","these","they","this","those",
                  "through","to","too","under","until","up","ve","very","was","wasn","wasn't","we","were","weren","weren't","what","when","where","which","while","who","whom","why","will",
                  "with","won","won't","wouldn","wouldn't","y","you","you'd","you'll","you're","you've","your","yours","yourself","yourselves","could","he'd","he'll","he's","here's","how's",
                  "i'd","i'll","i'm","i've","let's","ought","she'd","she'll","that's","there's","they'd","they'll","they're","they've","we'd","we'll","we're","we've","what's","when's",
                  "where's","who's","why's","would","able","abst","accordance","according","accordingly","across","act","actually","added","adj","affected","affecting","affects",
                  "afterwards","ah","almost","alone","along","already","also","although","always","among","amongst","announce","another","anybody","anyhow","anymore","anyone","anything",
                  "anyway","anyways","anywhere","apparently","approximately","arent","arise","around","aside","ask","asking","auth","available","away","awfully","b","back","became","become",
                  "becomes","becoming","beforehand","begin","beginning","beginnings","begins","behind","believe","beside","besides","beyond","biol","brief","briefly","c","ca","came","cannot",
                  "can't","cause","causes","certain","certainly","co","com","come","comes","contain","containing","contains","couldnt","date","different","done","downwards","due","e","ed",
                  "edu","effect","eg","eight","eighty","either","else","elsewhere","end","ending","enough","especially","et","etc","even","ever","every","everybody","everyone","everything",
                  "everywhere","ex","except","f","far","ff","fifth","first","five","fix","followed","following","follows","former","formerly","forth","found","four","furthermore","g","gave",
                  "get","gets","getting","give","given","gives","giving","go","goes","gone","got","gotten","h","happens","hardly","hed","hence","hereafter","hereby","herein","heres",
                  "hereupon","hes","hi","hid","hither","home","howbeit","however","hundred","id","ie","im","immediate","immediately","importance","important","inc","indeed","index",
                  "information","instead","invention","inward","itd","it'll","j","k","keep","keeps","kept","kg","km","know","known","knows","l","largely","last","lately","later","latter",
                  "latterly","least","less","lest","let","lets","like","liked","likely","line","little","'ll","look","looking","looks","ltd","made","mainly","make","makes","many","may",
                  "maybe","mean","means","meantime","meanwhile","merely","mg","might","million","miss","ml","moreover","mostly","mr","mrs","much","mug","must","n","na","name","namely","nay",
                  "nd","near","nearly","necessarily","necessary","need","needs","neither","never","nevertheless","new","next","nine","ninety","nobody","non","none","nonetheless","noone",
                  "normally","nos","noted","nothing","nowhere","obtain","obtained","obviously","often","oh","ok","okay","old","omitted","one","ones","onto","ord","others","otherwise",
                  "outside","overall","owing","p","page","pages","part","particular","particularly","past","per","perhaps","placed","please","plus","poorly","possible","possibly",
                  "potentially","pp","predominantly","present","previously","primarily","probably","promptly","proud","provides","put","q","que","quickly","quite","qv","r","ran","rather",
                  "rd","readily","really","recent","recently","ref","refs","regarding","regardless","regards","related","relatively","research","respectively","resulted","resulting",
                  "results","right","run","said","saw","say","saying","says","sec","section","see","seeing","seem","seemed","seeming","seems","seen","self","selves","sent","seven","several",
                  "shall","shed","shes","show","showed","shown","showns","shows","significant","significantly","similar","similarly","since","six","slightly","somebody","somehow","someone",
                  "somethan","something","sometime","sometimes","somewhat","somewhere","soon","sorry","specifically","specified","specify","specifying","still","stop","strongly","sub",
                  "substantially","successfully","sufficiently","suggest","sup","sure","take","taken","taking","tell","tends","th","thank","thanks","thanx","thats","that've","thence",
                  "thereafter","thereby","thered","therefore","therein","there'll","thereof","therere","theres","thereto","thereupon","there've","theyd","theyre","think","thou","though",
                  "thoughh","thousand","throug","throughout","thru","thus","til","tip","together","took","toward","towards","tried","tries","truly","try","trying","ts","twice","two","u",
                  "un","unfortunately","unless","unlike","unlikely","unto","upon","ups","us","use","used","useful","usefully","usefulness","uses","using","usually","v","value","various",
                  "'ve","via","viz","vol","vols","vs","w","want","wants","wasnt","way","wed","welcome","went","werent","whatever","what'll","whats","whence","whenever","whereafter","whereas",
                  "whereby","wherein","wheres","whereupon","wherever","whether","whim","whither","whod","whoever","whole","who'll","whomever","whos","whose","widely","willing","wish","within",
                  "without","wont","words","world","wouldnt","www","x","yes","yet","youd","youre","z","zero","a's","ain't","allow","allows","apart","appear","appreciate","appropriate",
                  "associated","best","better","c'mon","c's","cant","changes","clearly","concerning","consequently","consider","considering","corresponding","course","currently","definitely",
                  "described","despite","entirely","exactly","example","going","greetings","hello","help","hopefully","ignored","inasmuch","indicate","indicated","indicates","inner","insofar",
                  "it'd","keep","keeps","novel","presumably","reasonably","second","secondly","sensible","serious","seriously","sure","t's","third","thorough","thoroughly","three","well",
                  "wonder"}
    
    for i in data:
        if i not in stop_words:
            text.append(i)

    return(text)

#-  -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -

def get_frequency(formatted_data):          #get frequencies of each word in every document

    text_list = []
    count=0
    text_frequency = {}
    
    for i in formatted_data:
        if i not in text_list:
            for j in formatted_data:
                if i==j:
                    count = count+1
            text_frequency[i]=count
            count=0
            text_list.append(i)

    return(text_frequency,text_list)
      
#-  -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -       -

super_text_frequency = {}
super_text_list = []
formatted_word_list = []
matrix = {}

for documents in document_list:         #formatting the word list
    
    raw_data=''
    data =''
    formatted_data=''
    text_list = []
    text_frequency ={}
    

    for lines in documents:
        raw_data = raw_data+lines

    data = normalize_the_document(raw_data)
    formatted_data = stopwords_removal(data)
    text_frequency,text_list = get_frequency(formatted_data)

    super_text_list.append(text_list)
    super_text_frequency[documents] = text_frequency

for list in super_text_list:
    for word in list:
        if word not in formatted_word_list:
            formatted_word_list.append(word)
            

formatted_word_list.sort()

for docs in super_text_frequency:
    text_list = []
    for word in formatted_word_list:
        if word in super_text_frequency[docs]:
            text_list.append(super_text_frequency[docs][word])
        elif word not in super_text_frequency[docs]:
            text_list.append(0)
            
    super_text_frequency[docs] =  text_list;

#super_texted_frequency-> key - document, value - frequency list of formatted_word_list in key
    
#-  -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -       -

TF_matrix = {}
TF_list = []

for i,j in super_text_frequency.items():            # TF vector calculation
    TF_list = []
    count=0
    for k in j:
        if k!=0:
            count = count+1
    for k in j:
        TF_list.append(k/count)

    TF_matrix[i] = TF_list

#-  -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   

IDF_matrix = {}
index=-1
count = 0
word_list = {}

for words in formatted_word_list:                   #IDF vector calculation
    
    index = index+1
    count = 0
    
    for i,j in super_text_frequency.items():

        if j[index]!=0:
            count = count+1
            
    IDF_matrix[index] = round((math.log(5/count)),3)
    word_list[index] = words

#-  -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -

TF_sum = []
index = -1

for words in formatted_word_list:                   # TF sum calculation
    
    summ = 0
    term = 0
    index = index +1
    
    for i,j in TF_matrix.items():
        term = j[index]
        summ = term+summ
        
    TF_sum.append(summ)
        

#-  -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
    
temp1 = 0
temp2 = " "
temp3 = 0.0
temp4 = 0.0

n = len(word_list)-2

for i in range(0,n-1):                              # Selecting TOP 20 keywords using TF_sum sorting
    for j in range(i+1,n-i):
        
        if TF_sum[j]<TF_sum[j+1]:                   #sorting TF sum
            
            temp1 = TF_sum[j+1]
            TF_sum[j+1] = TF_sum[j]
            TF_sum[j] = temp1

            temp2 = word_list[j+1]                  #sorting the wordlist
            word_list[j+1] = word_list[j]
            word_list[j] = temp2

            temp3 = IDF_matrix[j+1]
            IDF_matrix[j+1] = IDF_matrix[j]         #sorting the IDF matrix
            IDF_matrix[j] = temp3

            for d in TF_matrix:                     #sorting the TF matrix
                temp4 = TF_matrix[d][j+1]
                TF_matrix[d][j+1] = TF_matrix[d][j]
                TF_matrix[d][j] = temp4


#-  -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -       -   -
                
TF_IDF_matrix = {}
TF_IDF_list = []
n_word_list = []

for i in range(20):                                 # TF*IDF for top 20 keyword matrix calculation
    n_word_list.append(word_list[i])

for i in TF_matrix:
    
    TF_IDF_list = []
    
    for k in range(20):
        TF_IDF_list.append(TF_matrix[i][k]*IDF_matrix[k])

    TF_IDF_matrix[i] = TF_IDF_list
    

for i in TF_IDF_matrix:

    summ = 0
    TF_IDF_list = []
    for elements in TF_IDF_matrix[i]:
        summ = summ+ pow(elements,2)
    for elements in TF_IDF_matrix[i]:
        TF_IDF_list .append(round((elements/pow(summ,0.5)),3))
    TF_IDF_matrix[i] = TF_IDF_list
    
#-  -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -

query = input("\n\nEnter te query: ")            #query vector generation and normalization
query_list = []
query_list = (query.split(" "))
query_vector = []
n = 0

for i in n_word_list:
    
    if i in query_list:
        query_vector.append(1.0)
        n = n+1
    else:
        query_vector.append(0.0)

summ=0
flag = 0
print("\nThe Query list: ",query_list)
print('\n')
if(n==0):
    print("\nThe given query is not present in the top 20 keywords of the corpus.\n")
    flag=1
    print("Top 20 keywords in the corpus:")
    for i in n_word_list:
        print(i)
    
    
     
elif(n!=0):
    n=n+1
    for i in range(20):
        ele = query_vector[i]*IDF_matrix[i]
        ele = ele/(n-1)
        query_vector[i] = ele
        summ = summ+ pow(ele,2)

    for i in range(20):
        ele = query_vector[i]
        query_vector[i] = (ele/pow(summ,0.5))

#-  -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
    
def cosine_similarity(q,d):                     #calculating cosine simmilarity between query and document 
    mod_q = 0
    mod_d = 0
    sum_q = 0
    sum_d = 0
    
    for i in range(20):
        sum_q = sum_q+pow(q[i],2)
        sum_d = sum_d+pow(d[i],2)

    mod_q = (pow(sum_q,0.5))
    mod_d = (pow(sum_d,0.5))
    
    sim = 0
    summ = 0

    for i in range(20):
        summ = summ+(q[i]*d[i])

    sim = (summ/(mod_q*mod_d),3)

    return(sim)
#-  -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -

similarity = []
similar = {}                        #comparing query with every document

if(flag==0):
    for i in TF_IDF_matrix:                                     
        similar[i] = cosine_similarity(query_vector,TF_IDF_matrix[i])
        similarity.append(similar[i])
    
    for i in similarity:                #result of comaprision between query and each document
        print(i)
    
#-  -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -   -
#END
