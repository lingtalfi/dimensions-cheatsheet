Dimensions of an element cheatsheet
=============================
2016-09-29


This [article on MDN](https://developer.mozilla.org/en-US/docs/Web/API/CSS_Object_Model/Determining_the_dimensions_of_elements)
explains the theory behind how to access the dimensions of an element in javascript.




In order to verify that the theory was applicable in current browsers, 
I've run this [test page](http://codepen.io/lingtalfi/pen/BLdBdL)
on multiple browsers:

- chrome53
- ff49
- safari9
- edge13 (via virtual box)
- ie11 (via virtual box)




Conclusion
===============

The theory works well in practice for most cases (see notes below).

- offsetWidth/offsetHeight: dimensions of the layout border box
- boundingClientRect: dimensions of the rendering border box
- clientWidth/clientHeight: dimensions of the visible part of the layout padding box (excluding scroll bars)
- scrollWidth/scrollHeight: dimensions of the layout padding box if it wasn't constrained by scroll bars


Note: apart from the boundingClientRect's height value (299.9999694824219 instead of expected 300) in edge13 and ie11,
the results confirm that the theory behind this works.

Note2: the boundingClientRect method has the following properties in all tested browsers: top, right, bottom, left, width, height.
In ff49, there are those two extra properties: x, y.

Note3: the vertical scroll bar's width is 12px in edge13, 15px in chrome53, ff49 and safari9, and 17px in ie11



Fixture
==============


```css
.div1{
    width: 500px;
    height: 300px;
    padding: 10px;
    border: 5px solid black;
    overflow: auto;
}
.div2{
    width: 500px;
    height: 300px;
    padding: 10px;
    border: 5px solid black;
    box-sizing: border-box;
    overflow: auto;
}

.div3{
    width: 500px;
    height: 300px;
    padding: 10px;
    border: 5px solid black;
    overflow: auto;
    transform: scale(0.5);
}
```

Each div contains 10 paragraph of lorem ipsum text.


ALL TESTS RESULTS
======================

- div1
    - offsetWidth: 530 (chrome53, ff49, safari9, edge13, ie11)
    - offsetWidth: 330 (chrome53, ff49, safari9, edge13, ie11)
    - bcr.width: 530 (chrome53, ff49, safari9, edge13, ie11)
    - bcr.height: 330 (chrome53, ff49, safari9, edge13, ie11)

    - clientWidth: 505 (chrome53, ff49, safari9)
    - clientWidth: 508 (edge13)
    - clientWidth: 503 (ie11)
    - clientHeight: 320 (chrome53, ff49, safari9, edge13, ie11)

    - scrollWidth: 505 (chrome53, safari9, ff49)
    - scrollWidth: 508 (edge13)
    - scrollWidth: 503 (ie11)
    - scrollHeight: 916 (chrome53, safari9)
    - scrollHeight: 954 (ff49)
    - scrollHeight: 922 (edge13, ie11)


- div2
    - offsetWidth: 500 (chrome53, ff49, safari9, edge13, ie11)
    - offsetWidth: 300 (chrome53, ff49, safari9, edge13, ie11)
    - bcr.width: 500 (chrome53, ff49, safari9, edge13, ie11)
    - bcr.height: 300 (chrome53, ff49, safari9)
    - bcr.height: 299.9999694824219 (edge13, ie11)
    - clientWidth: 475 (chrome53, ff49, safari9)
    - clientWidth: 478 (edge13)
    - clientWidth: 473 (ie11)
    - clientHeight: 290 (chrome53, ff49, safari9, edge13, ie11)

    - scrollWidth: 475 (chrome53, safari9, ff49)
    - scrollWidth: 478 (edge13)
    - scrollWidth: 473 (ie11)
    - scrollHeight: 916 (chrome53, safari9)
    - scrollHeight: 954 (ff49)
    - scrollHeight: 922 (edge13, ie11)

- div3
    - offsetWidth: 530 (chrome53, ff49, safari9, edge13, ie11)
    - offsetWidth: 330 (chrome53, ff49, safari9, edge13, ie11)
    - bcr.width: 265 (chrome53, ff49, safari9, edge13, ie11)
    - bcr.height: 165 (chrome53, ff49, safari9, edge13, ie11)
    - clientWidth: 505 (chrome53, ff49, safari9)
    - clientWidth: 508 (edge13)
    - clientWidth: 503 (ie11)
    - clientHeight: 320 (chrome53, ff49, safari9, edge13, ie11)

    - scrollWidth: 505 (chrome53, safari9, ff49)
    - scrollWidth: 508 (edge13)
    - scrollWidth: 503 (ie11)
    - scrollHeight: 916 (chrome53, safari9)
    - scrollHeight: 954 (ff49)
    - scrollHeight: 922 (edge13, ie11)




TEST DETAILS
====================

TEST 1: offsetWidth/offsetHeight and boundingClientRect
---------------------------------------------------------------

offsetWidth/offsetHeight: dimensions of the layout border box.
bounding client rect: dimensions of the rendering border box.


![offset](https://mdn.mozillademos.org/files/347/Dimensions-offset.png)


### chrome53, ff49, safari9

- div1
    - offsetWidth: 530
    - offsetWidth: 330
    - bcr.width: 530
    - bcr.height: 330
- div2
    - offsetWidth: 500
    - offsetWidth: 300
    - bcr.width: 500
    - bcr.height: 300
- div3
    - offsetWidth: 530
    - offsetWidth: 330
    - bcr.width: 265
    - bcr.height: 165

### edge13, ie11
- div1
    - offsetWidth: 530
    - offsetWidth: 330
    - bcr.width: 530
    - bcr.height: 330
- div2
    - offsetWidth: 500
    - offsetWidth: 300
    - bcr.width: 500
    - bcr.height: 299.9999694824219
- div3
    - offsetWidth: 530
    - offsetWidth: 330
    - bcr.width: 265
    - bcr.height: 165


I tested with a window size larger than 600 and lower than 300.
Results are the same.


TEST 2: clientWidth/clientHeight
---------------------------------------------------------------


Dimensions of the visible part of the layout padding box (excluding scroll bars).

![clientWidth/Height](https://developer.mozilla.org/@api/deki/files/185/=Dimensions-client.png)



### chrome53, ff49, safari9
- div1
    - clientWidth: 505
    - clientHeight: 320
- div2
    - clientWidth: 475
    - clientHeight: 290
- div3
    - clientWidth: 505
    - clientHeight: 320


### edge13
- div1
    - clientWidth: 508
    - clientHeight: 320
- div2
    - clientWidth: 478
    - clientHeight: 290
- div3
    - clientWidth: 508
    - clientHeight: 320

### ie11
- div1
    - clientWidth: 503
    - clientHeight: 320
- div2
    - clientWidth: 473
    - clientHeight: 290
- div3
    - clientWidth: 503
    - clientHeight: 320


Note that the vertical scroll bar's width is:
- edge13: 12px 
- chrome53, ff49 and safari9: 15px
- ie11: 17px




TEST 3: scrollWidth/scrollHeight
---------------------------------------------------------------

Dimensions of the layout padding box if it wasn't constrained by scroll bars.


### chrome53, safari9
- div1
    - scrollWidth: 505
    - scrollHeight: 916
- div2
    - scrollWidth: 475
    - scrollHeight: 916
- div3
    - scrollWidth: 505
    - scrollHeight: 916

### ff49
- div1
    - scrollWidth: 505
    - scrollHeight: 954
- div2
    - scrollWidth: 475
    - scrollHeight: 954
- div3
    - scrollWidth: 505
    - scrollHeight: 954


### edge13
- div1
    - scrollWidth: 508
    - scrollHeight: 922
- div2
    - scrollWidth: 478
    - scrollHeight: 922
- div3
    - scrollWidth: 508
    - scrollHeight: 922


### ie11
- div1
    - scrollWidth: 503
    - scrollHeight: 922
- div2
    - scrollWidth: 473
    - scrollHeight: 922
- div3
    - scrollWidth: 503
    - scrollHeight: 922



