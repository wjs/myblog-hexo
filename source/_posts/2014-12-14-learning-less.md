title: less笔记
date: 2014-12-14 23:13:08
tags:
---

这周末看了一下[慕课网的less视频](http://www.imooc.com/learn/102)，稍微记一下，虽然自己平时不用 = =  

1. 注释 `// comment` 或者 `/* comment */`
2. 变量 `@color-bg: #fff`
3. 混合 一个class里面可以直接使用另一个class。 带参数的混合。   
        // 不带参数的，直接调用其他class
        .class_a {
          width: 100px;
        }
        .class_b {
          .class_a;
          height: 50px;
        }
        // 带参数的混合，没有默认值的时候，调用必须要传参数
        .class_c(@w) {
          width: @w;
        }
        .class_d {
          .class_c(30px);
          height: 50px;
        }
        // 带默认值的混合，调用可以不用带参数
        .class_c(@w:100px) {
          width: @w;
        }
        .class_d {
          .class_c();
          height: 50px;
        } 

4. 匹配模式，类似if else  
        .fl(left) {
          float: left;
        }
        .fl(right) {
          float: right;
        }
        // 始终回匹配到的
        .fl(@_) {
          overflow: hidden;
        }
        // 调用
        .class_a {
          .fl(left);
        }

5. 运算
        // 有单位的属性，只要有一个带单位就可以了
        @test = 300px
        .class_a {
          width = (@test + 20) + 100px;
          height = @test / 2;
        }

6. 嵌套
        .class-a {
          float: left;
          a {
            display: block;

            // & 代表它的上一层，相当于和上一层直接拼接
            &:hover {

            }
          }

          // 这个就相当于 .class-a-b
          &-b {

          }
        }

6. @arguments 
7. 避免编译, !important
        width: ~'calc(300px-10px)';
        // !important 调用混合的时候，相当于里面每条语句都加上了!important
        .test(@w:100px) {
          float: left;
          width: @w;
        }
        .class-a {
          .test() !important;
        }
        // 相当于
        .class-a {
          float: left !important;
          width: 100px !important;
        }