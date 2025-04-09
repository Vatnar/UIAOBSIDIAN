```
```
@startuml
state initial
state s0
state s1
state s2
state s3
state s4 [[Output: Yes]]

[*] --> s0
s0 -- 0 --> s1
s0 -- 1 --> s0
s1 -- 0 --> s2
s1 -- 1 --> s0
s2 -- 0 --> s3
s2 -- 1 --> s0
s3 -- 0 --> s4
s3 -- 1 --> s0
s4 -- 0 --> s4
s4 -- 1 --> s0

@enduml