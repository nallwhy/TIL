## Tell, Don't Ask

> Procedural code gets information then makes decisions. Object-oriented code tells objects to do things. 
— Alec Sharp

You should **tell** objects what you want them to do; do not **ask** them questions about their state, make a decision, and then tell them what to do.

Object-orientation is about bundling data with the functions that operate on that data.

```java
class Monitor...
  private int value;
  private int limit;
  private boolean isTooHigh;
  private String name;
  private Alarm alarm;

  public Monitor (String name, int limit, Alarm alarm) {
    this.name = name;
    this.limit = limit;
    this.alarm = alarm;
  }

# Ask way

  public int getValue() {return value;}
  public void setValue(int arg) {value = arg;}
  public int getLimit() {return limit;}
  public String getName()  {return name;}
  public Alarm getAlarm() {return alarm;}

AskMonitor am = new AskMonitor("Time Vortex Hocus", 2, alarm);
am.setValue(3);
if (am.getValue() > am.getLimit())
  am.getAlarm().warn(am.getName() + " too high");

# Tell way

class TellMonitor...
  public void setValue(int arg) {
    value = arg;
    if (value > limit) alarm.warn(name + " too high");
  }

TellMonitor tm = new TellMonitor("Time Vortex Hocus", 2, alarm);
tm.setValue(3);

```

**Warning**: One thing I find troubling about tell-dont-ask is that I've seen it encourage people to become *GetterEradicators*, seeking to get rid of all query methods. But there are times when objects collaborate effectively by providing information.

Reference:  
https://pragprog.com/articles/tell-dont-ask  
https://martinfowler.com/bliki/TellDontAsk.html
