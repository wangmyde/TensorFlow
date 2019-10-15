### 1. How does TensorFlow work
Step 1: TensorFlow defines computations as Graphs, and these are made with operations.
Step 2: To execute these operations as computations, we must launch the Graph into a Session. 

#### Importing TensorFlow
```
import tensorflow as tf
```
#### Building a Graph
```
graph1 = tf.Graph() # create a graph which we named as graph1
```
#### Add tf.Operation and tf.Tensor objects to **graph1**
```
with graph1.as_default():
    a = tf.constant([2], name = 'constant_a')
    b = tf.constant([3], name = 'constant_b')
```
**Notice**: tf.constant([2], name="constant_a") creates a new tf.Operation named "constant_a" and returns a tf.Tensor named "constant_a:0".
#### Run in a session
##### Eg.1
```
sess = tf.Session(graph = graph1)
result = see.run(a)
print(result)
sess.close()
```
##### Eg.2
```
with graph1.as_default():
    c = tf.add(a, b)
    
sess = tf.Session(graph = graph1)
result = sess.run(c)
print(result)
sess.close()
```
To avoid having to close sessions every time, we can define them in a with block, so after running the with block the session will close automatically:
```
with tf.Session(graph = graph1) as sess:
    result =sess.run(c)
    print(result)
```
### 2. Defining multidimensional arrays using TensorFlow
```
graph2 = tf.Grapf()
with graph2.as_default():
    scalar = tf.constant(2)
    vector = tf.constant([1,2,3])
    matrix = tf.constant([[1,2,3],[4,5,6]])
    tensor = tf.constant([[1,2,3],[4,5,6],[7,8,9]], [[1,2,3],[4,5,6],[7,8,9]], [[1,2,3],[4,5,6],[7,8,9]])

with tf.Session(graph = graph2) as sess:
    result = sess.run(scalar)
    print("scalar is: " % result)
    result = sess.run(vector)
    print("vector is: " % vector)
```
#### Calculation of arrays
```
graph3 = tf.Graph()
with graph3.as_default():
    matrix_1 = tf.constant([[1,2,3],[4,5,6]])
    matric_2 = tf.constant([[6,5,4],[3,2,1]])
    add_operation_1 = tf.add(matrix_1, matrix_2)
    add_operation_2 = matirx_1 + matrix_2
    multiplication = tf.matmul(matrix_1, matrix_2)

with tf.Session(grahp = graph3) as sess:
    result = sess.run(add_operation_1)
    print(result)
```

### 3. Variables
Step 1: To define variables we use the command tf.Variable().
Step 2: To be able to use variables in a computation graph it is necessary to initialize them before running the graph in a session, *tf.global_variables_initializer()*
```
variable  = tf.Variable(0)
update = tf.assign(variable, variable + 1) # tf.assign takes in two arguments, the reference_variable to update, and assign it to the                                              # value_to_update it by.

init_op = tf.global_variables_initializer()

with tf.Session() as session:
    session.run(init_op)
    print(session.run(variable))
    for _ in range(3）：
        session.run(update)
        print(session.run(variable)
 ```
 
 ### Placeholders
Placeholders can be seen as "holes" in your model, "holes" which you will pass the data to, you can create them using
*tf.placeholder(datatype)*
##### Eg.1
```
a = tf.placeholder(tf.float32)
b = a * 2
with tf.Session() as sess:
    result = sess.run(b, feed_dict = {a:3.5})   
    print(result)
```
To pass the data into the model we call the session with an extra argument feed_dict in which we should pass a dictionary with each placeholder name followed by its respective data.

##### Eg.2
```
dictionary = {a: [[1,2],[3,4]]}
with tf.Session() as sess:
    result = sess.run(b, feed_dict = dictionary)
    print(result)
    

