
# One Time Pad


In this exercise we will implement the one-time pad. This is a type of
encryption which is impossible to crack (if you don't have the pad)! 

To use this encryption method, we take a `plaintext` string, for example ``THISISMYSECRETCODE``\ , and encrypt it using a `key`\ , for 
example, ``SUPERSECRETKEYKEEPMESAFE``. For a one-time pad to work, we need the key to be longer than the plaintext.

.. note:: 
  
    We will use the convention that `key` and `plaintext` should be **uppercase**, 
    while `ciphertexts` should be **lowercase** for testing. The `key` will not contain spaces,
    but the `plaintext` and the `ciphertext` may.


The code is simple in concept. First, we consider mapping letters to numbers:

```
======   ========   ====== ======
Letter   Number     Letter Number
======   ========   ====== ======
A         0           P     15
B         1           Q     16
C         2           R     17
D         3           S     18
E         4           T     19
F         5           U     20
G         6           V     21
H         7           W     22
I         8           X     23
J         9           Y     24
K         10          Z     25
L         11          
M         12           
N         13           
O         14           
======   ========   ====== ======

```

This allows us to convert both our `key` and `plaintext` into a list of numbers.
For example:

.. math::
    
    key = SUPERSECRETKEYKEEPMESAFE &= \mathtt{18\ 20\ 15\  4\ 17 \ldots} \\
    plaintext = THISISMYSECRETCODE &= \mathtt{19\  7\  8\ 18\  8\ \ldots}
    
To encipher, using the one-time pad, we add up the numbers:

.. math::
  
  \mathtt{37\ 27\ 23\ 22\ 25 \ldots }

Take the modulo of each number around 26:

.. math::  
  
  \mathtt{11\ 1\ 23\ 22\ 25 \ldots }
  
and then convert these numbers back to letters:

.. math::
    
    ciphertext = \mathtt{ l b x w z \ldots}

"""

qs1 = SubQuestion()
qs1.subquestion_no = "a - Ciphering"
qs1.header_rst = r"""

In this exercise, we will need to introduce another basic type, :class:`char`.  :class:`char` represents a single letter, similar to 
Haskell.

To implement the ciphering and deciphering using the one-time pad, you
will create a class :class:`OneTimePadEncipher`. We have given the skeleton
for this class below:

.. code-block:: java

    public class OneTimePadEncipher {

	public static int charToInt(char l) {    
	  // ADD CODE HERE
	  // Should convert a character to an integer, for example 'a' -> 0, 'b' -> 1
	}

	public static char intToChar(int i) {
	  // ADD CODE HERE
	  // Should convert an integer to a character, for example 0 -> 'a', b -> '1'
	  // it should always return lower case chae
	}

	public static boolean isAlpha(char c) {
	  // You do not need to implement this method, but you may find it useful.
	}

	public static String encipher(String original, String onetimepad) {
	  // ADD CODE HERE
	}


	public static void main(String[] args) {
	  String ciphertext = encipher("HELLO EVERYBODY", "MYSECRETKETMYSECRETKEY");
	  System.out.print(ciphertext);
	}

    }


Notes: 
  
  * You should be careful that your `plaintext` and your `key` are
    both in uppercase. You can use the :class:`String` method
    :func:`toUpperCase` and :func:`toLowerCase` to convert a string
    to upper or lowercase. Note that this method returns a new string,
    so it must be **assigned**. E.g., ``mystring =
    mystring.toLowerCase;``.

  * To extract a :class:`char` from a :class:`String` at a certain
    index, you can use the :func:`String.charAt` method on the :class:`String`
    object. For example, ``char c = "hello".charAt(2);``, will set
    ``c=l`` .

  * It is possible to convert a :class:`char` into an :class:`int` using
    *casting*.  However, note that this will give the `ascii` value
    of the letter. For example ``(int) ('a') -> 97, (int) ('b') -> 98,
    (int) ('A') -> 65``.

  * Think about what to do in the case of spaces in the plaintext;
    they should be spaces in the output (This is not good for making
    the code secure, but makes human reading easier!). Unit tests will
    assume that you ignore the values in the one-time pad at the
    indices of the spaces.




If everything is sucessful, you should be able to encrypt the following:

```
==================   ======================   ==================
Plaintext            Key                      Ciphertext
==================   ======================   ==================
HELLO                XMCKL                    eqnvz
SUPERSECRETMESSAGE   MYSUPERDUPERSECRETCKEY   eshygwvfltxdwwurkx
IS THIS SECURE       KEEPMEVERYVERYSAFE       sw itmn jcxyic
==================   ======================   ==================
```



qs2 = SubQuestion()
qs2.subquestion_no = "b - Deciphering"
qs2.header_rst = r"""

Create a new class :class:`OneTimePadDecipher` and implement a method
to decrypt `ciphertext` given a key. To decrypt a code, you need to
**subtract** the key from the ciphertext representation, instead of
adding it.

You can cut-and-paste the methods you already defined so that they are
also available in this class. 

.. note:: 

    Be careful with the ``%`` operator on negative numbers. ``-4 % 26``
    is not 22 as you might expect. To be careful, you can add 26 to
    possibly negative numbers, before taking the modulo of them, which
    will ensure they are positive, but not change the result.


The signature of the new method is as follows:

.. code-block:: java

    public static String decipher(String encipheredText, String onetimepad)



If everything is sucessful, you should be able to decrypt the following:

```
==================   ============================   
Ciphertext           Key                      
==================   ============================   
uvufsghktdal         WHATSTHEPASSWORD
wconlahzgzgleuai     YOULLNEVERREADMYONETIMEPAD
==================   ============================
```

"""

u1 = Submission( label="OneTimePad", expected_filename="OneTimePadEncipher.java",identifier="T6Q7Sub1" )
u2 = Submission( label="OneTimePad", expected_filename="OneTimePadDecipher.java",identifier="T6Q7Sub2" )

modelans1 = ModelAnswer(
    contents = ReadFromFile(ConfigFile.get().getJavaModelFilesDir() + "/lab5/Q3/OneTimePadEncipher.java" )
    )

modelans2 = ModelAnswer(
    contents = ReadFromFile(ConfigFile.get().getJavaModelFilesDir() + "/lab5/Q3/OneTimePadDecipher.java" )
    )

    
Q = QuestionWrapper( identifier='T6Q7',  question = q, subquestions =
[qs1,qs2], submissions = [u1, u2] )

Q.addModelAnswer( submission = u1, modelanswer = modelans1 )
Q.addModelAnswer( submission = u2, modelanswer = modelans2 )


Q.addJUnitTestWrapper( 
    filename=ConfigFile.get().getJavaTestFilesDir()+"/lab5/Q3/OneTimePadTestEnciphering.java", 
    subquestion = qs1,
    submission = u1,
    jumethodnames = {
          "testEnciphering1":"Test Enciphering Key: XMCKL",
          "testEnciphering2":"Test Enciphering Key: MYSUPERDUPERSECRETCKEY",
          "testEnciphering3":"Test Enciphering Key: KEEPMEVERYVERYSAFE",
          }, 
    jupackagename = "lab1.Q2", 
    marks=1 )

Q.addJUnitTestWrapper( 
    filename=ConfigFile.get().getJavaTestFilesDir()+"/lab5/Q3/OneTimePadTestDeciphering.java", 
    subquestion = qs2,
    submission = u2,
    jumethodnames = {
          "testDeciphering1":"Test Deciphering Key: WHATSTHEPASSWORD",
          "testDeciphering2":"Test Deciphering Key: YOULLNEVERREADMYONETIMEPAD",
          "testDeciphering3":"Test Deciphering Key: KEEPMEVERYVERYSAFE",
          }, 
    jupackagename = "lab1.Q2", 
    marks=1,
    supportfiles = [ConfigFile.get().getJavaTestFilesDir() + '/lab5/Q3/OneTimePadEncipher.java'] )



