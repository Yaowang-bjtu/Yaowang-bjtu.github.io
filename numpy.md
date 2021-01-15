# Numpy

## The Basics

NumPy’s main object is the homogeneous multidimensional array.
It is called `ndarray`.
In Numpy dimensions are called *axes*. The number of axes is *rank*.

```
[[ 1., 0., 0.],
[ 0., 1., 2.]]
```

The above array has rank 2. The first dimension has a length of 2, the second dimension has a length of 3.

The more important attributes of an ndarray object are:

| attributes | description |
|------------|-------------|
|`ndim`|the number of axes |
|`shape`|the size of the array in each axes|
|`size`| the total number of elements|
|`dtype`|the type of the elements|
|`itemsize`|the size in **bytes** of each element|
|`data`|the buffer containing the actual elements|

### Array Creation

There are several ways to create arrays:

* Create an array from a regulay Python list or tuple using the `np.array` function.
* Create arrays with initial placeholder content.
  * `np.zeros`
  * `np.ones`
  * `np.empty`
* Create sequences of numbers
  * `np.arange`
  * `np.linspace`

### Basic Operations

Arithmetic operators on arrays apply *elementwise*. A new arrray is created and filled with the result.

The matrix product can be performed  using the `dot` function or method:

```python
A = np.array( [[1,1],
               [0,1]])
B = np.array( [[2,0],
              [3,4]] )
A.dot(B)           
np.dot(A, B)
```

Some operations, such as `+=` and `*=`, act in place to modify an existing array rather than create a new one.

Many unary operations, such as computing the sum of all the elements in the array, are implemented as methods of the `ndarray` class.

```
>>> a = np.random.random((2,3))
>>> a
array([[ 0.18626021, 0.34556073, 0.39676747],
       [ 0.53881673,  0.41919451,  0.6852195 ]])
>>> a.sum() 2.5718191614547998
>>> a.min() 0.1862602113776709
>>> a.max() 0.6852195003967595
```

By default, these operations apply to the array as though it were a list of numbers, regardless of its shape. However, by specifying the axis parameter you can apply an operation along the specified axis of an array:

### Universal Functions

NumPy provides familiar mathematical functions such as sin, cos, and exp. In NumPy, these are called “universal functions”(ufunc). Within NumPy, these functions operate elementwise on an array, producing an array as output.

### Indexing, Slicing and Iterating

**One-dimensional** arrays can be indexed, sliced and iterated over, much like lists and other Python sequences.

**Multidimensional** arrays can have one index per axis. These indices are given in a tuple separated by commas.

The dots (...) represent as many colons as needed to produce a complete indexing tuple. For example, if x is a rank 5 array (i.e., it has 5 axes), then

* `x[1,2,...]` is equivalent to `x[1,2,:,:,:]`
* `x[...,3]` to `x[:,:,:,:,3]`
* `x[4,...,5,:]` to `x[4,:,:,5,:]`

Iterating over multidimensional arrays is done with respect to the first axis:
if one wants to perform an operation on each element in the array, one can use the `flat` attribute.

## Shape Manipulation

### Changing the shape of an array
The shape of an array can be changed with various commands:

|commands|description|
|:---------:|----------|
|`a.ravel()`|flatten the array(return a new array)|
|`a.T`|Transposition|
|`a.resize()`|modifies the shape of the array itself|
|`a.shape=(6,2)`|same to a.resize()|
|`a.reshape()`|return a new array with a modified shape|

If a dimension is given as -1 in a reshaping operation, the other dimensions are automatically calculated.

### Stacking together different arrays

Several arrays can be stacked together along different axes:

|commands|description|
|:---------:|----------|
|`np.vstack()`| stacks along their first axes|
|`np.hstack()`| stacks along their second axes|
|`np.concatenate()`|allows for an optional arguments giving the number of the axis along which the con- catenation should happen.|
|`np.column_stack()`|stacks 1D arrays as columns into a 2D array|
|`np.r_()`and `np.c_()`|They allow the use of range literals (”:”) |

### Splitting arrays

|commands|description|
|:---------:|----------|
|`np.hsplit()`|split an array along its horizontal axis|
|`np.vsplit()`|splits along the vertical axis|
|`np.array_split()`|allows one to specify along which axis to split|

## Copies and Views

### No Copy at all

Simple assignments make no copy of array objects or of their data.

Python passes mutable objects as references, so function calls make no copy.

### View or Shallow copy

Different array objects can share the same data. The `view` method creates a new array object that looks at the same data.
(their shapes can be different, and their data is the same)

### Deep copy

The `copy` method makes a complete copy of the array and its data.

## Fancy indexing and index tricks

### Indexing with Arrays of Indeces

可以用数组索引数组，得到的数组：
* 形状与索引数组形状相同
* 数值为索引数组对应位置数值作为索引，从被索引数组获取到的值
* 当被索引数组为多维数组时，索引该数组的第一维

```
>>> a = np.arange(12)**2
>>> i = np.array( [ 1,1,3,8,5 ] )
>>> a[i]
array([ 1, 1, 9, 64, 25])
>>>
>>> j=np.array([[3,4],[9,7]]) >>> a[j]
array([[ 9, 16],
[81, 49]])
```

When the indexed array `a` is multidimensional, a single array of indices refers to the first dimension of `a`.

### Indexing with Boolean Arrays

用布尔数组索引
* 从被索引数组中选择出布尔数组对应位置是True的数组，组成新的数组。
* 如果被索引数组是多维数组，可以单独取某一维度，其它维度用`:`索引即可。

## Linear Algebra
### Simple Array operations
|commands|description|
|:---------:|----------|
|`a.transpose()`|转置|
|`np.eye()`|生成单位矩阵|
|`np.dot()`|矩阵乘法|
|`np.trace()`|矩阵的迹|
|`np.linalg.solve()`|求解线性方程式|
|`np.linalg.eig()`|求解矩阵的特征向量,特征值|
