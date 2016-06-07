# yii2-chartjs-widget
Yii2 Chart widget with support for chart.js 2.0.

## Installation

To install the widget in your application, run

    composer require enscope/yii2-chartjs-widget:~1.0

or add

    "enscope/yii2-chartjs-widget" : "~1.0"

to the require section of your application's composer.json file.

It is possible to use the source code directly, but it is recommended to use `composer`, for your own good.

## Basic Usage

Main class of the widget is `ChartJsWidget`, which is the only one you need in your views.
Basic configuration goes like this:

    {ChartJsWidget::widget([
        'chartType' => ChartJsWidget::CHART_LINE,
        'canvasOptions' => [
            'height' => 200
        ],
        'chartOptions' => [
            'animation' => false,
            'bezierCurve' => false,
            'maintainAspectRatio' => false,
            'responsive' => true,
            'tooltips' => [
                'callbacks' => [
                    'label' => ChartJsWidget::js('function (item) { return (item.yLabel + "%"); }')
                ]
            ]
        ],
        'chartData' => $chartData
    ])}

All supported chart types are defined as constants:

    const CHART_LINE = 'line';
    const CHART_BAR = 'bar';
    const CHART_RADAR = 'radar';
    const CHART_POLAR_AREA = 'polarArea';
    const CHART_PIE = 'pie';
    const CHART_DOUGHNUT = 'doughnut';

To include javascript callbacks in configuration, `ChartJsWidget::js(..)` helper is available to allow for simple expression instantiation even for users, who are using `Smarty` as a templating engine for their app (like in this case). The helper simply instantiates `yii\web\JsExpression` with specified string.

The properties of the widget are as follows:

- **$id** is user-definable HTML5 Canvas identifier for the widget, but can be left blank and is auto-generated in that case
- **$canvasOptions** are the HTML attributes directly injected into the `<canvas>` tag
- **$chartType** is one of the before-mentioned chart types supported by chart.js library (in case, there are some new chart types and the widget is lagging behind, you can always freely use strings as chart type names, but it is recommended to use the constants)
- **$chartData** is the data of the chart, directly set to `data` key of the `Chart()` configuration
- **$chartOptions** are the configuration `options` of the chart

## Planned Enhancements

- support of global chart defaults
- chart-specific data and options classes to simplify instantiation

## Acknowledgments

This widget was inspired by [2amigOS! ChartJs widget](http://github.com/2amigos/yii2-chartjs-widget), which unfortunatelly was not available for chart.js 2.0, so I decided to create a new one with some inspiration borrowed in terms of basic structure.
