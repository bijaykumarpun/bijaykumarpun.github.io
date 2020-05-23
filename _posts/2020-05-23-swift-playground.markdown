---
layout: post
title: "Swift Playground Test Session 1"
categories: [programming, swift“]
---

import UIKit

var str = "Hello, playground"


//MARK: bnrg

//swift types are of three basic groups: structures, classes and enumerations
//All have
// - properties, i.e values associated with a type
// - initializers - code that initializes an instance of a type
// instance methods - functions specific to a type that can be called on an instance of that type
// class or static methods - functions specific to a type that can be called on the type itself


str = "Hello, Swfit"
let constStr = str

//MARK: type inference

var name = "Hari bahadur"


//MARK: type declaration

var nextYear: Int = 0
var bodyTemp: Float = 0
var hasPet: Bool = true


//MARK: collection types
//arrays, dictionaries and sets

//arrays
var arrayOfInts: Array<Int> = []
//or shorthand method
var arrayOfIntsShortHand: [Int] = []
var arrayOfStrings: [String] = []
var arrayOfStringsLongHand: Array<String> = []

//dictionaries
//AN unorderd collection of key-value paris

var dictionaryOfCapitalsByCountry: Dictionary<String,String> = [:]
//or
var dictionaryShort:[String:String] = [:]


//set
var winningLotteryNumbers: Set<Int> = []
//no shorthand version



//MARK: Literals and Subscripting

let number = 45
let fmStation = 92.4

//assigning literals to arrays nad dictionaries
let countingUp = ["one","two"]
let nameByParkingSpace = [13:"Alice", 25:"bob"]

//subscripting
let secondElement = countingUp[1]


//MARK: initializers

//initializer is a way of creating instance of class, enumerations or structures


let emptyString = String()
let emptyArrayOfInts = [Int]()
let emptySetOfFloats = Set<Float>()
//Other types have default values
let defaultNumber = Int()
let defaultBool = Bool()

//types can have multiple initiazliers
//eg for string
var num = 10
var namedNum = String(num)
let availableRooms = Set([204,205,206]) // a set

//eg for float
var pii = Float()
var piii = Float(4.44)



//MARK: Properties


let counter:[Int]  = [1,3,4]
counter.count //property

let fullName:String = "Ram bahadur"
var isEmpty:Bool = fullName.isEmpty


//MARK: Instance methods


var countingDown = ["three","two","one"]
countingDown.count
countingDown.append("zero")
var carray = Array(["ram","sam"])
carray.count


//MARK: Optionals

//Optional allows variable to either have a value or have nil, which means no value at all

var anOptionalFloat: Float?
var anOptionalArrayOfStrings: [String]?
var anOptionalArrayOfOptionalStrings: [String?]?

var reading1: Float?
var reading2: Float?
var reading3: Float?

reading1 = 2.2
reading2 = 4.4 //if this is nil, it will cause a trap
reading3 = 4.4

//though these optional variables can be assied just as easily as normal variables, they can't however be read easily
//they need to be `unwrapped` first i.e addressing the possibility of them being null

//There are two ways of unwrapping an optional
// Optional binding and forced unwrapping

//forced unwrapping
var ag:Float = (reading1! + reading2! + reading3!)/3


//optional binding

if let r1 = reading1,let  r2 = reading2, let r3 = reading3{
    let avg = (r1+r2+r3)/3
    print(avg)
} else {
    print("Error in the code")
}


