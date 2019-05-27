# add-binary
//this is a problem from leetcode 67
//description:
//Given two binary strings, return their sum (also a binary string).
//The input strings are both non-empty and contains only characters 1 or 0.

public static String addBinary(String a,String b) {
			int  bit = 0; 
			if(a.length()<b.length()) {
				 String str = a;
				 a = b;
				 b = str;
			}
			StringBuffer sb = new StringBuffer();
			for(int i=0;i<a.length()-b.length();i++){
				sb.append('0');
			}
			for(int i=0;i<b.length();i++){
				sb.append(b.charAt(i));
			}
 			b =sb.toString();
	    	int[] a1 = new int[a.length()];
	    	a1[a1.length-1]=a.charAt(a.length()-1)+b.charAt(b.length()-1)-96;
	    	if(a1[a1.length-1]==2) {
	    		bit = 1;
	    		a1[a1.length-1] = 0;
	    	}//对个位数进行计算并对bit赋初值
	    	for(int i = 1;i<a.length();i++) {
	    		if(bit == 1||bit ==2) {
	    			bit = 0;
	    			a1[a1.length-1-i]=a.charAt(a.length()-1-i)+b.charAt(b.length()-1-i)-95;
	    			}
	    		else {
	    			bit= 0;
	    			a1[a1.length-1-i]=a.charAt(a.length()-1-i)+b.charAt(b.length()-1-i)-96;
	    			}
	    		if(a1[a1.length-1-i]==2) {
	    			a1[a1.length-i-1]=0;
	    			bit = 1;
	    			}
	    		if(a1[a1.length-1-i]==3) {
	    			a1[a1.length-i-1]=1;
	    			bit = 2;
	    			}
	    	}
	    	if(bit == 1||bit ==2) {
	    		int res[] = new int[a.length()+1];
				res[0] = 1;
				for(int i = 0;i<a1.length;i++) {
					res[i+1] = a1[i];
				}
				StringBuffer buf = new StringBuffer();
	 			for(int i=0;i<res.length;i++){
	 			   buf.append(res[i]);
	 			}
	    		return buf.toString();
	    	}	  
	    	else {
	    		StringBuffer buf = new StringBuffer();
	 			for(int i=0;i<a1.length;i++){
	 				buf.append(a1[i]);
		 		}
	 			return buf.toString();
	 		}
  }
  
  //the first one is very complex,first,I zeroes the shorter strings to make them equal in length,.then iterate through the two strings, determine whether to add, and determine whether to carry by bit variable.
  
		public static String addBinary1(String a,String b) {
			if(a.length()<b.length()) {
				 String str = a;
				 a = b;
				 b = str;
			}
			StringBuffer sb = new StringBuffer();
            if(a.length()>b.length()){
                for(int i=0;i<a.length()-b.length();i++){
				    sb.append('0');
			    }
			    for(int i=0;i<b.length();i++){
				    sb.append(b.charAt(i));
			    }
 			    b =sb.toString();
            }

	    	int[] a1 = new int[a.length()];	
	    	a1[a.length()-1] = a.charAt(a.length()-1)+b.charAt(b.length()-1)-96;
	    	if (a.length()>1) {
		    	for(int i = a.length()-2;i>=0;i--) {
		    		a1[i] = a.charAt(i)+b.charAt(i)+a1[i+1]/2-96;
		    		a1[i+1] = a1[i+1]%2;
		    	}
	    	}
	    	if(a1[0]/2 ==1) {
	    		a1[0] = a1[0]%2;
	    		int res[] = new int[a.length()+1];
				res[0] = 1;
				for(int i = 0;i<a1.length;i++) {
					res[i+1] = a1[i];
				}
				StringBuffer buf = new StringBuffer();
	 			for(int i=0;i<res.length;i++){
	 			   buf.append(res[i]);
	 			}
	    		return buf.toString();
	    	}	  
	    	else {
	    		StringBuffer buf = new StringBuffer();
	 			for(int i=0;i<a1.length;i++){
	 				buf.append(a1[i]);
		 		}
	 			return buf.toString();
	 		}
	    }  
      
      //the second one uses mod and strives for the remainder by 2,to determine the value of the current bit and whether carry plus one.
      
      public static String addBinary2(String a,String b) {
			
			long a10 = 0;
			for(int i = a.length()-1; i >= 0  ; i--) {
				a10+=(a.charAt(i)-48)*Math.pow(2,a.length()-i-1);
			}
			long b10 = 0;
			for(int i = b.length()-1; i >= 0  ; i--) {
				b10+=(b.charAt(i)-48)*Math.pow(2,b.length()-i-1);
			}
			long sum = a10+b10;
			ArrayList<Integer> arr = new ArrayList<Integer>();
			while(sum>1) {
				int n = 0;
				n= (int) (sum%2);
				arr.add(n);
				sum = sum/2;
			}
            int m= (int) (sum%2);
            arr.add(m);		
			StringBuffer buf = new StringBuffer();
			for(int i = arr.size()-1;i >=0;i--){
				buf.append(arr.get(i));
			}
			return buf.toString();
	    }
      //I hope to transform to decimal number sum it up  and then convert to binary .but I failed,because it over the range.
      
		public static String addBinary3(String a,String b) {
			int bit = 0;
			StringBuffer result = new StringBuffer();
			int al = a.length()-1;
			int bl = b.length()-1;
			while(al>=0||bl>=0) {
				int u = 0;
				int d = 0;
				if(al>=0) {
					u = a.charAt(al)-'0';
				}
				if(bl>=0) {
					d =b.charAt(bl)-'0'; 
				}
				int nowP=(u+d+bit)%2;
				result.append(nowP);
				bit = (u+d+bit)>>1;
			al--;
			bl--;
			}
			if(bit!=0) {
				result.append('1');
			}
			return result.reverse().toString();
	    }
		//the last one is more concise 
      
