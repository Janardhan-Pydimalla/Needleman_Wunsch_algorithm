# Needleman_Wunsch_algorithm

"""
Created on Sun Sep  6 12:39:21 2020

@author: Janardhan
"""








def needle6():

    gap=int(input("Enter the gap penality: "))
    
    match=int(input("Enter the match score: "))
    mismatch=int(input("Enter the mismatch penality: "))
    print("\nEnter the sequences. Copy & Paste the fasta file content :- ")
    
    Content1=input("\nEnter the first sequence : ")
    Counter1 = 0
    # Reading from file 
    CoList1 = Content1.split("\n") 
    for i in CoList1: 
        if i: 
            Counter1 += 1
    x1=Content1.splitlines()
    string1=x1[1]
    for i in range(2,Counter1):
        string1=string1+x1[i]
    print("\nString1 is\n",string1)
    
    Content2=input("Enter the second sequence : \n")
    Counter2 = 0
    # Reading from file 
    CoList2 = Content2.split("\n") 
    for i in CoList2: 
        if i: 
            Counter2 += 1
    x2=Content2.splitlines()
    string2=x2[1]
    for i in range(2,Counter2):
        string2=string2+x2[i]
    print("\nString2 is\n",string2)
    
    l1=len(string1)
    l2=len(string2)
    print("\nThe lengths of the sequences are ",l1,l2,end='.')
    print("\n\n")
    
    string1=string1[::-1]
    string2=string2[::-1]
    
    space=0
    score=[[0 for i in range(l1+1)] for j in range(l2+1)]
    tb=[[[space,space,space] for i in range(l1+1)] for j in range(l2+1)]
    

    for j in range(1,l2+1):
        for i in range(1,l1+1):
            score[j][0]=score[j-1][0]+gap
            score[0][i]=score[0][i-1]+gap
            tb[j][0][2]=1
            tb[0][i][1]=1
    
    for j in range(1,l2+1):
        for i in range(1,l1+1):
            if(string1[i-1]==string2[j-1]):
                m=match
            else:
                m=mismatch
            s0=score[j-1][i-1]+m
            s1=score[j][i-1]+gap
            s2=score[j-1][i]+gap
            score[j][i]=max(s0,s1,s2)
            s=score[j][i]
            if(s==s0):
                tb[j][i][0]=1
            else:
                tb[j][i][0]=0
            if(s==s1):
                tb[j][i][1]=1
            else:
                tb[j][i][1]=0
            if(s==s2):
                tb[j][i][2]=1
            else:
                tb[j][i][2]=0
    #print("\n",score)
    #print("\n",tb)
    gene1=" "+string1
    gene2=" "+string2
    
    mc=0
    x=l1
    y=l2
    nxt=tb[l2][l1]
    
    as1=""
    as2=""
    bar=""

    for l in range(l1+l2):
        if(x<-2):
            break
        if(y<-2):
            break
        if(nxt[0]==1):
            as1+=gene1[x]
            as2+=gene2[y]
            if(gene1[x]==gene2[y]):
                mc=mc+1
                bar+="|"
            else:
                bar+=" " 
            x-=1
            y-=1
            nxt=tb[y][x]
            continue
        else:
            pass
        
        if(nxt[1]==1):
            as1+=gene1[x]
            as2+="_"
            bar+=" "
            x-=1
            nxt=tb[y][x]
            continue
        else:
            pass
      
        if(nxt[2]==1):
            as1+="_"
            as2+=gene2[y]
            bar+=" "
            y-=1
            nxt=tb[y][x]
            continue
        else:
            as1+="."
            as2+="."
            bar+="."
            break
        
    #as1=as1[::-1]
    #as2=as2[::-1]
    #bar=bar[::-1]
    
    k=0
    j=0
    while(j<l):
        ag1=""
        br=""
        ag2=""
        for j in range(0+100*k,99+100*k):
            if(as1[j]=='.'):
                break
            ag1+=as1[j]
        print(ag1)
        for j in range(0+100*k,99+100*k):
            if(bar[j]=='.'):
                break
            br+=bar[j]
        print(br)
        for j in range(0+100*k,99+100*k):
            if(as1[j]=='.'):
                break
            ag2+=as2[j]
        print(ag2)
        print("\n")
        k+=1
        
    
    #print("\n")
    #print(ag1)
    #print(br)
    #print(ag2)
    #print("\n")
    if l2>l1:
        l1=l2
    print("The number of matches is ",mc)
    print("The percent similarity is ",mc*100/l1)
