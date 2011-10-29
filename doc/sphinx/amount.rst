
Amount
======

The Amount include contains all kinds of functions to get the amount of items.
Items can be in your bank or in your inventory.


TradeScreen
~~~~~~~~~~~

.. code-block:: pascal

    function TradeScreen: Integer;

Returns 1 if the first trade screen is open, 2 if the second, and 0 if neither
is open.

.. note::

    Author: ZephyrsFury
    Last Modified: Unknown

Example:

.. code-block:: pascal

    if (TradeScreen > 0) then
    writeln('Trade screen is open!');

ShopScreen
~~~~~~~~~~

.. code-block:: pascal

    Function ShopScreen : Boolean;

Returns true if the shop screen is open.

.. note::

    Author: ZephyrsFury
    Last Modified: Unknown by NCDS

Example:

.. code-block:: pascal

    if (ShopScreen) then
    writeln('Shop screen is open!');

FindItemEx
~~~~~~~~~~

.. code-block:: pascal

    function FindItemEx(var x, y: Integer; IdentType: string; Ident: Integer; Area: TBox; Tol: TIntegerArray): Boolean;

Finds an item in a specified box (Area). Returns its coordinates (x, y).
Valid IdentTypes are:

   - 'bmp', 'mask', 'color', 'dtm'

The Tol variable is:

   Tol[0] : Color Tolerance;
   Tol[1] : Contour Tolerance or minimum Colors to Find to be True.

.. note::

    Author: Nava2
    Last Modified: 13 Jan 2011 by Nava2

Example:

.. code-block:: pascal

    var
      x, y: Integer;
      b: TBox;
    begin
      b:= IntToBox(MIX1, MIY1, MIX2, MIY2);
      if (FindItemEx(x,y, 'bmp, the_bmp, b, [4])) then
        Mouse(x, y, 5, 5, true);
    end;

FindItem
~~~~~~~~

.. code-block:: pascal

    function FindItem(var x, y: Integer; IdentType: string; Ident: Integer; x1, y1, x2, y2: Integer; Tol: TIntegerArray): Boolean;

This function is exactly the same as FindItemEx except it takes integer
coordinates (x1, y1, x2, y2) rather than an TBox.

.. note::

    Author: Nava2
    Last Modified: Unknown

Example:

.. code-block:: pascal

    var
      x, y: Integer;
    begin
      if (FindItem(x,y, 'bmp, the_bmp, MIX1, MIY1, MIX2, MIY2, [4])) then
        Mouse(x, y, 5, 5, true);
    end;

GetAmountBox
~~~~~~~~~~~~

.. code-block:: pascal

    function GetAmountBox(box: TBox): integer;

Returns the amount of an item at in the box 'box'. Returns approximate values
for 'K' and 'M'.

.. note::

    Author: Zeph, N1ke & Narcle
    Last Modified: Unknown

Example:

.. code-block:: pascal

    var
      i: Integer;
    begin
      i := GetAmountBox(InvBox(1)); // Gets the amount in inventory slot 1
    Writeln('Amount = '+toStr(i));
    end;

GetAmount
~~~~~~~~~

.. code-block:: pascal

    function GetAmount(x, y: integer): integer;

Returns the amount of an item at inventory coordinates (x, y).

.. note::

    Author: Coh3n
    Last Modified: Unknown

Example:

.. code-block:: pascal

    var
      amount, x, y: integer;
  begin
    if (findDTM(x, y, dtm_Hatchet, MIX1, MIY1, MIX2, MIY2)) then
    begin
      amount := GetAmount(x, y);
      writeln('amount: '+toStr(amount));
    end;
    end;

AreaInfo
~~~~~~~~

.. code-block:: pascal

    procedure AreaInfo(area: String; var startx, starty, rowsize, colsize, colnumber, rownumber: Integer);

Returns information on certain interfaces.  Valid interfaces (area):

  - 'inv'
  - 'inventory'
  - 'trade'
  - 'your trade'
  - 'bank'
  - 'shop'
  - 'deposit box'

.. note::

    Author: masquerader
    Last Modified: Unknown by Mr. Freeweed

Example:

.. code-block:: pascal

    var
      info: array[0..5] of integer;
  begin
    AreaInfo('inv', info[0], info[1], info[2], info[3], info[4], info[5]);
    end;

CheckArea
~~~~~~~~~

.. code-block:: pascal

    function CheckArea(area: String): Boolean;

Checks if the given area is opened.

.. note::

    Author: masquerader
    Last Modified: Unknown by EvilChicken

Example:

.. code-block:: pascal

    if (CheckArea('shop')) then
    writeln('Shop is open!');

ItemCoordinates
~~~~~~~~~~~~~~~

.. code-block:: pascal

    function ItemCoordinates(Area, ItemType: string; Item, Tol: TIntegerArray): TPointArray;

Returns a TPA with the positions of all occurances of the item.
Parameters:
  Area - 'inv', 'shop', 'bank', 'trade', 'your trade'.
  ItemType - DTM, Color, BitmapMask, Bitmap
  Item - name/value of your dtm/bmp/color/bmpmask.
  Tol - 'dtm' - [] (dtm's can't have tolerance).
        'bmp' - [BMPTol].
        'color' - [COLOUR Tol, Minimum Colour Count].
        'bmpmask' - [BMPTol, ContourTol].

.. note::

    Author: masquerader
    Last Modified: Unknown by ZephyrsFury

Example:

.. code-block:: pascal

    if (length(ItemCoordinates('inv', 'dtm', dtm_Hatchet, []) > 0) then
    writeln('Hatchet found!');

CountItemsIn
~~~~~~~~~~~~

.. code-block:: pascal

    function CountItemsIn(Area, ItemType: string; Item: Integer; Tol: TIntegerArray): Integer;

Counts the number of items found within the Area (does not count stacks).
Parameters are exactly the same as ItemCoordinates.

.. note::

    Author: masquerader
    Last Modified: Unknown by ZephyrsFury

Example:

.. code-block:: pascal

  var
    itemsFound: integer;
  begin
      itemsFound := CountItemsIn('inv', 'dtm', dtm_Ore, []);
    writeln('Ore found: '+toStr(itemsFound));
  end;

CountItemsArea
~~~~~~~~~~~~~~

.. code-block:: pascal

    function CountItemsArea(area: string): Integer;

Counts the number of items (no matter which item) found in the given area. Looks
for the black outline color.

.. note::

    Author: masquerader
    Last Modified: Unknown

Example:

.. code-block:: pascal

  var
    itemsFound: integer;
  begin
      itemsFound := CountItemsArea('inv');
    writeln('Items found: '+toStr(itemsFound));
  end;

ItemAmount
~~~~~~~~~~

.. code-block:: pascal

    function ItemAmount(area, ItemType: string; Item: Integer; Tol: TIntegerArray): Integer;

Counts the number of items found within the Area (counts stacks).
Parameters are exactly the same as ItemCoordinates.

.. note::

    Author: masquerader
    Last Modified: Unknown by ZephyrsFury

Example:

.. code-block:: pascal

  var
    itemsFound: integer;
  begin
      itemsFound := ItemAmount('inv', 'dtm', dtm_Ore, []);
    writeln('Ore found: '+toStr(itemsFound));
  end;

FindCoins
~~~~~~~~~

.. code-block:: pascal

    function FindCoins(var X, Y: Integer; Area: string): Boolean;

Returns true if coins are found in the given area (Area). If found, stores their
coordinates in X, Y.

.. note::

    Author: ZephyrsFury
    Last Modified: Unknown

Example:

.. code-block:: pascal

  var
    x, y: integer;
  begin
    if (FindCoins(x, y, 'inv')) then
      writeln('Coins found: '+toStr(GetAmount(x, y)));
  end;

CoinAmount
~~~~~~~~~~

.. code-block:: pascal

    function CoinAmount(Area: string): Integer;

Returns the amount of coins found in the given area.

.. note::

    Author: ZephyrsFury
    Last Modified: Unknown

Example:

.. code-block:: pascal

  writeln('Coins found: '+toStr(CoinAmount('inv')));

RuneAmount
~~~~~~~~~~

.. code-block:: pascal

    function RuneAmount(area, runetype: String): Integer;

Returns the amount of a certain rune in the specified area.

.. note::

    Author: masquerader
    Last Modified: Unknown by ZephyrsFury

Example:

.. code-block:: pascal

  writeln('Air runes found: '+toStr(RuneAmount('inv', 'air')));

ShopSwitchTab
~~~~~~~~~~~~~

.. code-block:: pascal

    procedure ShopSwitchTab(Name: string);

Switches the shop tab to the one you want, only moves mouse if neccessary.
Valid arguments are:

  - ShopSwitchTab('main')
  - ShopSwitchTab('player')

.. note::

    Author: Rasta Magician & ZephyrsFury
    Last Modified: Unknown by ZephyrsFury

Example:

.. code-block:: pascal

  ShopSwitchTab('main');
