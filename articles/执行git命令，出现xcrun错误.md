title: 执行git命令，出现xcrun错误
author: 骑马揍比尔
tags:
  - git
  - xcrun
  - xcode-select
categories:
  - git
date: 2019-01-17 16:44:00
---




在执行git命令的时候出现

> xcrun: error: invalid active developer path (/Library/Developer/CommandLineTools), missing xcrun at: /Library/Developer/CommandLineTools/usr/bin/xcrun

我出现这种问题是在升级mac系统版本后出现的。是由于xcode问题造成的，可在终端中执行如下命令

> xcode-select --install

<!--more-->


pre, code {
    display: block;
    background: none repeat scroll 0 0;
    background-color: #555555;
    border-radius:4px 4px 4px 4px;
    box-shadow: rgba(0, 0, 0, 0.25) 0px 0px 10px inset;
    clear: both;
    font-family: Andale Mono,AndaleMono,monospace; 
    color: #fff;
    /*background-color: #f8f8f8;*/
    margin: 5px 0px;
    overflow: auto;
    padding: 10px;
    font-size:14px;
    white-space: pre;
    /*text-indent: 1em;*/
}
table,tbody,tr{
  display: block !important;
}
td {
  display: inline-block !important;
}
.code{
  width: calc(100% - 60px);
}


