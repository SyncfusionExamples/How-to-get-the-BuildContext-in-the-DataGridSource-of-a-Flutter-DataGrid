# How to get the BuildContext in the DataGridSource of a Flutter DataGrid (SfDataGrid)?.

In this article, we will show you how to get the BuildContext in the DataGridSource of a [Flutter DataGrid](https://www.syncfusion.com/flutter-widgets/flutter-datagrid).

Initialize the [SfDataGrid](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/SfDataGrid-class.html) widget with all the necessary properties. You can achieve this by maintaining the build context in the [DataGridSource](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/DataGridSource-class.html). In the [initState](https://api.flutter.dev/flutter/widgets/State/initState.html) method, pass the context to the DataGridSource so that you can access the [BuildContext](https://api.flutter.dev/flutter/widgets/BuildContext-class.html) within the DataGridSource.

```dart
 List<Employee> employees = <Employee>[];
  late EmployeeDataSource employeeDataSource;

  @override
  void initState() {
    super.initState();
    employees = getEmployeeData();
    employeeDataSource = EmployeeDataSource(employees, context);
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Syncfusion Flutter DataGrid'),
      ),
      body: SfDataGrid(
        source: employeeDataSource,
        columnWidthMode: ColumnWidthMode.fill,
        columns: getColumns     
       ),
    );
  }

In DataGridSource:

class EmployeeDataSource extends DataGridSource {
  /// Creates the employee data source class with required details.
  EmployeeDataSource(List<Employee> employeeData, this.context) {
    _employeeData = employeeData
        .map<DataGridRow>((e) => DataGridRow(cells: [
              DataGridCell<int>(columnName: 'id', value: e.id),
              DataGridCell<String>(columnName: 'name', value: e.name),
              DataGridCell<String>(
                  columnName: 'designation', value: e.designation),
              DataGridCell<int>(columnName: 'salary', value: e.salary),
            ]))
        .toList();
  }

BuildContext context;

  @override
  DataGridRowAdapter buildRow(DataGridRow row) {
    return DataGridRowAdapter(
        color: Theme.of(context).primaryColor,
        cells: row.getCells().map<Widget>((e) {
          return Container(
            alignment: Alignment.center,
            padding: const EdgeInsets.all(8.0),
            child: Text(e.value.toString()),
          );
        }).toList());
  }
}
```

You can download this example on [GitHub](https://github.com/SyncfusionExamples/How-to-get-the-BuildContext-in-the-DataGridSource-of-a-Flutter-DataGrid).