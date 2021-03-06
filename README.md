# HiResStopWatch
High resolution stopwatch using RDTSCP. 

# Easy to use

```delphi
procedure TForm1.Button5Click(Sender: TObject);
const
  repeats = 1000000;
var
  Timer: THiResStopWatch;
  Time1, Time2: int64;
begin
  Time1:= Timer.Sample(TimeInRange, repeats, EmptyProc);
  Time2:= Timer.Sample(TimeCase, repeats, EmptyProc);
  Memo1.Lines.Add(Format('InRange takes %d cycles',[Time1]));
  Memo1.Lines.Add(Format('case takes %d cycles',[Time2]));
end;
```

`TimeInRange`, `TimeCase` and `EmptyProc` are simple procedures that look like:

```delphi
procedure TForm1.EmptyProc;
begin
end;
```

# Accurate  
Given enough repeats the timer is accurate to within 2 CPU cycles.  
The timer knows about out-of-order execution and eliminates this issue as per [Intel recommendations](http://www.intel.de/content/dam/www/public/us/en/documents/white-papers/ia-32-ia-64-benchmark-code-execution-paper.pdf).
The shorter the timing, the more repeats are needed.  

1.000.000 is normal for single cycle timings.  
100.000 for 100 cycle timings.  
and 10.000 for 1000 cycle timings  
etc.

If your code takes longer you might as well use the normal TStopWatch.  
