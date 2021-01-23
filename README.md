A binary gap within a positive integer N is any maximal sequence of consecutive zeros that is surrounded by ones at both ends in the binary representation of N.

For example, number 9 has binary representation 1001 and contains a binary gap of length 2. The number 529 has binary representation 1000010001 and contains two binary gaps: one of length 4 and one of length 3. The number 20 has binary representation 10100 and contains one binary gap of length 1. The number 15 has binary representation 1111 and has no binary gaps. The number 32 has binary representation 100000 and has no binary gaps.

Write a function:

    function solution(N);

that, given a positive integer N, returns the length of its longest binary gap. The function should return 0 if N doesn't contain a binary gap.

For example, given N = 1041 the function should return 5, because N has binary representation 10000010001 and so its longest binary gap is of length 5. Given N = 32 the function should return 0, because N has binary representation '100000' and thus no binary gaps.

Write an efficient algorithm for the following assumptions:

        N is an integer within the range [1..2,147,483,647].

Copyright 2009–2021 by Codility Limited. All Rights Reserved. Unauthorized copying, publication or disclosure prohibited.





*****************************************************************************************************************************




   
    
    // you can write to stdout for debugging purposes, e.g.
    //console.log('this is a debug message');
    
    function solution(N) {
    // write your code in JavaScript (Node.js 8.9.4)
    let aux = '';
    let cont = 0;
    let cont2 = 0;
    let numBi = (N.toString(2));
    let auxArr = [];
    //console.log(numBi);
    
     for(let i=0; i<numBi.length; i++){
        
        if(numBi.charAt(i) == '1' && cont != 1 && numBi.charAt(i+1) == '0'){
            aux += numBi.charAt(i);
            cont = 1;
        } else if (numBi.charAt(i) == '1' && cont == 1) {
            aux += numBi.charAt(i);
            auxArr[cont2] = aux;
            aux = numBi.charAt(i);
            cont = 0;
            cont2 ++;
        }
        if (numBi.charAt(i) == '0' && cont == 1){
            aux += numBi.charAt(i);
        }
        if (aux == '1' && cont == 0){
            cont = 1;
        }
 
    }

    //console.log(auxArr[0]);
    //console.log(auxArr[1]);

    let cont3 = 0;
    if (auxArr[0] != undefined){
    // metodo insertion-sort modificado
	    for (let i=0; i<auxArr.length; i++) {
		    let aux2 = auxArr[i];
		    let j = i - 1;
		    while (j >= 0 && auxArr[j].length > aux2.length) {
			    auxArr[j+1] = auxArr[j];
			    j--;
			    }
		    auxArr[j+1] = aux2;
	    }

        let result = auxArr[auxArr.length-1];
        for(let i=0; i<result.length; i++){
            if(result.charAt(i) == '0'){
                cont3 += 1;
            }
        }

    }

    return cont3;
}
