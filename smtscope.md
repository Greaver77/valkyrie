#smtscope

*   [Overview](#overview)
    *   [Starting smtscope](#starting-smtscope)
*   [Detailed Description](#detailed-description)
    *   [Topic Selector](#topic-selector)
    *   [Plot Area](#plot-area)
        *   [Basic controls](#basic-controls)
    *   [Plot Options](#plot-options)
    *   [Value Table](#value-table)

# **Overview**

**smtscope** is a GUI for plotting line smt data.
<img src="https://github.com/NASA-JSC-Robotics/valkyrie/wiki/images/smtscope.png">

## Starting smtscope

    smtscope
    -- or ---
    rosrun shared_memory_transport_qt smtscope

NOTE: There are no command line arguments, and no 'help'.

--[back to top](#smtscope)--

# Detailed Description

## Topic Selector

The topic selector provides a view of all the current plottable topics available on SMT.  The tree-view is the broken down hierarchically.  Shared Memory Topics use '/' to act as a name spacing of sorts of topic names.  While this "namespacing" doesn't actually mean anything to the actual transport, this tool uses this convention to help organize the data for the user.  When any level of the hierarchy is checked/unchecked, all sub-items of the tree will also be checked/unchecked.  

NOTE: If the highest-level of a hierarchy is selected of a fairly large tree, the system can take a very long time to refresh the screen. Use this feature with caution.  

At the top of the topic selector, there is a text box where a user can input a filter.  This filter must be formatted as a [regular expression](https://en.wikipedia.org/wiki/Regular_expression).  For those who aren't savvy with regex (which is MOST people), there are several online tools to help you cheat, line [this one](http://txt2re.com/).  The button next to the text box toggles case sensitivity in the filter.

## Plot Area

The graph area provides two different views of the data.  The large window on top is meant to be the primary view used by the user.  The view on the bottom is meant to be a "wide" or "zoomed-out" view of the data.

### Basic controls

*   **Panning** - press and hold left mouse button
*   **Zoom** - Scrolling the center wheel will <span style="line-height: 20.0px;">zoom all about the cursor.  Right-click hold and drag left/right or up/down to zoom in/out vertically and horizontally</span>
*   **<span style="line-height: 20.0px;">View all</span>** <span style="line-height: 20.0px;">- Right click once to pop-open a context menu.  Select "View All" to fit the screen to view all the data.</span>

## Plot Options

The check boxes below the plots modify how the views will update.  

*   **Autoscroll** - the plot will continually scroll from right-to-left, where the right-hand side of the plot will show the current time
*   **Show Crosshairs** - this will show a horizontal and vertical line intersecting with the cursor on the main plot.  The x, y value of the cursor will be displayed near the intersection point, where x is the time and y is the value.  While selected, the values in the table will reflect the value of the topic at the cursor's point in time
*   **Show Legend** - When selected, the legend for the different signals will be displayed in the upper left-hand corner of the main window

## Value Table

The value table provides the value of all the topics that are being plotted.  When **Show Crosshairs** is selected, the value will be at the point in time of the crosshairs, otherwise the most current value is displayed.

--[back to top](#smtscope)--