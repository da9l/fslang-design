
# F# 4.0+ Proposal for regularizing the functions defined for List, Array and Seq

There is an approved [proposal](https://fslang.uservoice.com/forums/245727-f-language/suggestions/5663997-make-fsharp-core-collection-functions-for-list-ar) to make the functions defined in the List, Array and Seq modules in FSharp.Core.dll more regular.

If you would like to work on one or more of these function implementations, please submit a PR to this document
adding an entry to column "assigned to" indicating you're willing to code, test and submit the the functions to 
http://visualfsharp.codeplex.com branch "fsharp4".  If you have questions, please tweet @dsyme, or raise an issue in this
forum, or discuss on fslang.uservoice.com.

The F# 2.x and 3.x philosophy for these functions was somewhat irregular. The majority of functions (e.g. map, filter, groupBy, averageBy) 
were defined for Seq, but some were not present on List and Array (e.g. groupBy).  This leads to awkward code where Seq-producing functions 
are used even when List is an input. Seq.groupBy is a particular example.

Also, some functions were not defined on Seq, even though they exist in List or Array. 

The proposal below is to complete the matrix for List, Array and Seq w.r.t. functional collection functions.


## Regular functional functions

| Function   | Comment   | List      | Array     | Seq      |   Assigned To       |    Status      |
|:-----------|:----------|:---------:|:---------:|:--------:|:--------:|:--------:|
| append     |           |     o     |    o      |    o     |   ---       |    ---      |
| average    |           |      o    |        o  |      o   |   ---       |  ---        |
| averageBy  |           |    o      |      o    |    o     |   ---       |  ---        |
| choose     |           |   o       |     o     |   o      |   ---       |  ---        |
| collect    |           |  o        |      o    |      o   |   ---       |  ---        |
| compareWith|           |  ADD      |     ADD   |     o    |          |          |
| concat     |           |     o     |       o   |     o    |   ---       | ---         |
| countBy    |           |  ADD      |     ADD   |      o   |          |          |
| distinct   |           |   ADD     |     ADD   |     o    |          |          |
| distinctBy |           |    ADD    |    ADD    |    o     |          |          |
| empty      |           |    o      |    o      |      o   |   ---       |   ---       |
| exactlyOne |           |    ADD    |    ADD    |        o |          |          |
| exists     |           |     o     |       o   |     o    |   ---       |   ---       |
| exists2    |           |    o      |        o  |      o   |   ---       |   ---       |
| filter     |           |   o       |     o     |     o    |   ---       |     ---     |
| find       |           |   o       |     o     |     o    |   ---       |     ---     |
| findIndex  |           |  o        |      o    |      o   | ---         |     ---     |
| fold       |           |     o     |     o     |     o    | ---         |     ---     |
| fold2      |           |   o       |    o      |     ADD  |          |          |
| foldBack   |           |   o       |    o      |   ADD    |          |          |
| foldBack2  |           |   o       |   o       |    ADD   |          |          |
| forall     |           |   o       |  o        |     o    |    ---      |   ---       |
| forall2    |           |  o        |   o       |      o   |   ---       |     ---     |
| groupBy    |           |    o      |       o   |    ADD   |          |          |
| head       |           |   o       |    ADD    |   o      |          |          |
| init       |           |   o       |    o      |     o    |   ---       |   ---       |
| isEmpty    |           |    o      |     o     |      o   |   ---       |     ---     |
| iter       |           |   o       |      o    |     o    |   ---       |     ---     |
| iter2      |           |    o      |       o   |    o     |   ---       |       ---   |
| iteri      |           |    o      |       o   |    o     |   ---       |     ---     |
| iteri2     |           |   o       |      o    |   ADD    |          |          |
| last       |           |   ADD     |    ADD    |     o    |          |          |
| length     |           |   o       |    o      |     o    |   ---       |   ---       |
| map        |           |    o      |     o     |      o   |   ---       |     ---     |
| map2       |           |   o       |    o      |     o    |   ---       |     ---     |
| map3       |           |   o       |    ADD    |   ADD    |          |          |
| mapi       |           |   o       |    o      |     o    |   ---       |     ---     |
| mapi2      |           |  o        |   o       |    ADD   |          |          |
| max        |           |    o      | o         |  o       |   ---       |     ---     |
| maxBy      |           |    o      | o         |    o     |   ---       |     ---     |
| min        |           |  o        |         o |  o       |   ---       |     ---     |
| minBy      |           |    o      |   o       |    o     |   ---       |     ---     |
| nth        |           |      o    | ADD       |  o       |          |          |
| pairwise   |           |     ADD   |    ADD    |     o    |          |          |
| permute    |           |    o      |       o   |    ADD   |          |          |
| pick       |           |     o     |        o  |     o    |   ---       |     ---     |
| reduce     |           |     o     |        o  |     o    |   ---       |     ---     |
| reduceBack |           |    o      |         o |      ADD |          |          |
| replicate  | cf. create |     o    |    ADD    |   ADD    |          |          |
| rev        |           |    o      |   o       |    ADD   |          |          |
| scan       |           |     o     |      o    |     o    | ---         |   ---       |
| scanBack   |           |     o     |    o      |   ADD    |          |          |
| singleton  |           |    ADD    |     ADD   |    o     |          |          |
| skip       |           |   ADD     |      ADD  |   o      |          |          |
| skipWhile  |           |  ADD      |     ADD   |    o     |          |          |
| sort       |           | o         |    o      |     o    |    ---      |   ---       |
| sortBy     |           |   o       |      o    |     o    |   ---       |   ---       |
| sorthWith  |           |    o      |    o      |  ADD     |          |          |
| sum        |           |    o      |   o       |   o      |   ---       |   ---       |
| sumBy      |           |    o      |   o       |   o      |   ---       |    ---      |
| tail       |           |    o      |  ADD      |  ADD     |          |          |  
| take       |           |    ADD    |   ADD     |  o       |          |          |
| takeWhile  |           |    ADD    |  ADD      | o        |          |          |
| truncate   |           |    ADD    | ADD       |  o       |          |          |
| tryFind    |           |    o      |  o        |  o       |   ---       | ---         |
| tryFindIndex |         |    o      | o         | o        |   ---       | ---         |
| tryPick    |           |    o      |  o        | o        |   ---       | ---         |
| unfold     |           |    ADD    | ADD       |  o       |          |          |
| where      | syn. filter |  ADD    |  ADD      |  o       |          |          |
| windowed   |           |    ADD    |  ADD      |  o       |          |          |
| zip        |           |    o      |  o        |  o       |   ---       |   ---       |
| zip3       |           |    o      |  o        |  o       |   ---       |   ---       |

Note: In F# 3.0 Seq.where was defined as a synonym for Seq.filter, mainly due to the use of "where" in query expressions. Given
it already  exists as a synonym (= decision made) it seems sensible to just complete the matrix and define List.where and Array.where as well.




## Regular functional operators producing two or more output collections 

These operators are not defined for Seq.* for performance reasons because using them would require iterating the input sequence twice.

| Note it is arguable that if these are not defined, then Seq.tail, Seq.skip and Seq.skipWhile should also not be defined, since
| they implicitly skip inputs and can be a performacne trap, especially when used recursively.

| Function   | Comment   | List      | Array     | Seq      |   xxxxxxxxxxxxxxxxxxx       |    xxxxxxxxxxxxxxx      |
|:-----------|:----------|:---------:|:---------:|:--------:|:--------:|:--------:|
| partition  |           |    o      |       o   |    n/a    |          |          |
| unzip      |           |    o      |   o       | n/a       |          |          |
| unzip3     |           |    o      |  o        | n/a       |          |          |

## Mutation-related operators

| Function   | Comment   | List      | Array     | Seq      |   xxxxxxxxxxxxxxxxxxx       |    xxxxxxxxxxxxxxx      |
|:-----------|:----------|:---------:|:---------:|:--------:|:--------:|:--------:|
| blit       |           |     n/a   |   o       |   n/a    |          |          |
| copy       |           |   n/a     |     o     |     n/a  |          |          |
| create     |           |   n/a     |      o    |    n/a   |          |          |
| fill       |           |   n/a     |     o     |     n/a  |          |          |
| get        |           |    n/a    |     o     |  n/a     |          |          |
| set        |           |    n/a    |   o       |    n/a   |          |          |
| sortInPlace  |         |    n/a    |    o      |   n/a    |          |          |
| sortInPlaceBy  |       |    n/a    |   o       |   n/a    |          |          |
| sortInPlaceWith  |     |    n/a    |    o      |   n/a    |          |          |
| sub        |           |    n/a    |   o       |  n/a     |          |          |
| zeroCreate |           |    n/a    |  o        |n/a       |          |          |

## Conversion operators

| Function   | Comment   | List      | Array     | Seq      |   xxxxxxxxxxxxxxxxxxx       |    xxxxxxxxxxxxxxx      |
|:-----------|:----------|:---------:|:---------:|:--------:|:--------:|:--------:|
| ofList     |           |   n/a     |    o      |   o      |          |          |
| ofArray    |           |      o    | n/a       |    o     |          |          |
| ofSeq      |           |      o    |       o   |    n/a   |          |          |
| toList     |           |    n/a    |  o        | o        |          |          |              
| toArray    |           |    o      |  n/a      |  o       |          |          |
| toSeq      |           |    o      | o         | n/a      |          |          |

## On-demand or IEnumerable computation operators

| Function   | Comment   | List      | Array     | Seq      |   xxxxxxxxxxxxxxxxxxx       |    xxxxxxxxxxxxxxx      |
|:-----------|:----------|:---------:|:---------:|:--------:|:--------:|:--------:|
| cache      |           |    n/a    |    n/a    |   o      |          |          |
| cast       |           |   n/a     |   n/a     |   o      |          |          |
| delay      |           |    n/a    |    n/a    |    o     |          |          |
| initInfinite |         |    n/a    |   n/a     |    o     |          |          |
| readonly   |           |     n/a   |      n/a  |   o      |          |          |