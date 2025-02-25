
![[Pasted image 20241002145903.png]]
![[Pasted image 20241002145925.png]]

## 1 . Step Function :
![[Pasted image 20241002150006.png]]

- Returns 1 if our input is greater than a threshold, otherwiae 0.
- Too simple and hence not usually used.

## 2. Sigmoid Function
![[Pasted image 20241002150155.png]]

- Outputs a probability between 0 and 1.
- If the input is a very negative number the Simoid outputs a number close to 0.
- If the input is a very positive number the Simoid outputs a number close to 1.
- Sometimes used in the hidden layers but most of the time it is used in the last layer for binary classification.

## 3. TanH (Hyperbolic Tangent) :
![[Pasted image 20241002150531.png]]

- Common choice for hidden layers. 
- Basically ==a scaled and shifted sigmoid function== that outputs a number between -1 and +1.

## 4. ReLU :
![[Pasted image 20241002150821.png]]

- Most popular choice in **hidden layers**.
- Takes maximum of 0 and input x. Basically return 0 if input is negative and outputs 1 if input is positove.

## 5. Leaky ReLu


## 6. Softmax :
![[Pasted image 20241002151137.png]]

 - Softmax squashes the input numbers to output numbers between 0 and 1 so that we will get a probability value at the end. 
 - Higher the raw input number, higher will be the probability value.
 - Usually used in last layer in multi-class classification.


![[Pasted image 20241002151946.png]]

<hr><hr>

**Hiden Layer :** 
- TanH
- ReLU
**Output/Last Layer :**
- Sigmoid (for binary classification)
- Softmax (for multi-class classification)