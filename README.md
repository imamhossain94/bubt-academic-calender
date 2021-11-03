# BUBT Academic Calender

### Tools used
* <a href="https://www.newocr.com/">NewOcr</a>
* <a href="https://jsonformatter.curiousconcept.com/#">Json Formatter</a>

### Data example
```json
{
   "semester":"Summer 2021",
   "semester_type":"Trimester",
   "data":[
      {
         "date":{
            "start":"09 Aug 2021",
            "end":"26 Aug 2021"
         },
         "day":{
            "start":"Monday",
            "end":"Thursday"
         },
         "activities":"Payment of tuition fees: 1st installment"
      },
      {
         "date":{
            "start":"15 Aug 2021",
            "end":"15 Aug 2021"
         },
         "day":{
            "start":"Sunday",
            "end":"Sunday"
         },
         "activities":"Holiday (National Mourning Day)"
      }
   ]
}
```

### Kotlin model
```kotlin
implementation "com.google.code.gson:gson:2.8.8"

val json = getJson()
val topic = Gson().fromJson(json, AcademicCalender::class.java)

data class AcademicCalender (
	@SerializedName("semester") val semester : String,
	@SerializedName("semester_type") val semester_type : String,
	@SerializedName("data") val data : List<Data>
)

data class Data (
	@SerializedName("date") val date : Date,
	@SerializedName("day") val day : Day,
	@SerializedName("activities") val activities : String
)

data class Date (
	@SerializedName("start") val start : String,
	@SerializedName("end") val end : String
)

data class Day (
	@SerializedName("start") val start : String,
	@SerializedName("end") val end : String
)
```

### Dart model
```dart
class AcademicCalculator {
  String semester;
  String semesterType;
  List<Data> data;

  AcademicCalculator({this.semester, this.semesterType, this.data});

  AcademicCalculator.fromJson(Map<String, dynamic> json) {
    semester = json['semester'];
    semesterType = json['semester_type'];
    if (json['data'] != null) {
      data = new List<Data>();
      json['data'].forEach((v) {
        data.add(new Data.fromJson(v));
      });
    }
  }

  Map<String, dynamic> toJson() {
    final Map<String, dynamic> data = new Map<String, dynamic>();
    data['semester'] = this.semester;
    data['semester_type'] = this.semesterType;
    if (this.data != null) {
      data['data'] = this.data.map((v) => v.toJson()).toList();
    }
    return data;
  }
}

class Data {
  Date date;
  Date day;
  String activities;

  Data({this.date, this.day, this.activities});

  Data.fromJson(Map<String, dynamic> json) {
    date = json['date'] != null ? new Date.fromJson(json['date']) : null;
    day = json['day'] != null ? new Date.fromJson(json['day']) : null;
    activities = json['activities'];
  }

  Map<String, dynamic> toJson() {
    final Map<String, dynamic> data = new Map<String, dynamic>();
    if (this.date != null) {
      data['date'] = this.date.toJson();
    }
    if (this.day != null) {
      data['day'] = this.day.toJson();
    }
    data['activities'] = this.activities;
    return data;
  }
}

class Date {
  String start;
  String end;

  Date({this.start, this.end});

  Date.fromJson(Map<String, dynamic> json) {
    start = json['start'];
    end = json['end'];
  }

  Map<String, dynamic> toJson() {
    final Map<String, dynamic> data = new Map<String, dynamic>();
    data['start'] = this.start;
    data['end'] = this.end;
    return data;
  }
}
```
