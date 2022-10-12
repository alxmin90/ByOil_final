unit Unit1;

interface

uses
  Windows, Messages, SysUtils, Variants, Classes, Graphics,
  Controls, Forms, Dialogs, StdCtrls, ComObj;

type
  TForm1 = class(TForm)
    Button2: TButton;
    Label1: TLabel;
    e0: TEdit;
    Label2: TLabel;
    Label3: TLabel;
    Label4: TLabel;
    e1: TEdit;
    e2: TEdit;
    Label5: TLabel;
    e3: TEdit;
    Azimut: TLabel;
    Label6: TLabel;
    Label7: TLabel;
    Label8: TLabel;
    e4: TEdit;
    e5: TEdit;
    e6: TEdit;
    procedure Button2Click(Sender: TObject);
  private
    { Private declarations }
  public
    { Public declarations }
  end;

const
   xlCellTypeLastCell = $0000000B;

var
  Form1: TForm1;
  f : TextFile;
  s: string;



implementation

{$R *.dfm}

Uses Math;


Type
  mas = array [1 .. 3] of String;

function split(s: String) : mas;
var
  count:Integer;
  i:integer;
  rez:mas;
  c:char;
Begin
  count := 1;
  rez[1] := '';
  i := 1;
  while (i <= Length(s)) do Begin
    c := s[i];
    if c = #9 Then Begin
      Inc(count);
      rez[count] := '';
    End else
      if not (c in [#10, #13]) Then Begin
        rez[count] := rez[count] + c;
      End;
    Inc(i);
  End;
  Result := rez;
End;


procedure TForm1.Button2Click(Sender: TObject);
var
  interval : Integer;
  plan1 : Real;
  plan2 : Integer;
  f : TextFile;
  finterval : Integer;

  num : Integer;
  symbol:  char;

  fakt1 : Real;
  fakt2 : Integer;

  itog1: Real;
  itog2: Real;

  str: String;
  numbers : mas;

  found: Boolean;
begin
  // Проверка на пустоту полей
  if (e0.Text = '') or (Trim(e0.Text) = '') Then
    Begin
      ShowMessage('Введите значение интервала');
      Exit;
    End;

  if (e1.Text = '') or (Trim(e1.Text) = '') Then
    Begin
      ShowMessage('Введите значение плана зенитного угла');
      Exit;
    End;

  if (e4.Text = '') or (Trim(e4.Text) = '') Then
    Begin
      ShowMessage('Введите значение плана азимута');
      Exit;
    End;

  Try
    interval := StrToInt(Trim(e0.Text));
  Except
    ShowMessage('Ошибка ввода интервала. Необходимо ввести целое число.');
    Exit;
  end;

  if interval < 0 Then Begin
    ShowMessage('Интервал должен быть больше либо равен 0.');
    Exit;
  End;

  Try
    plan1 := StrToFloat(Trim(e1.Text));
  Except
    ShowMessage('Ошибка ввода плана зенитного угла. Необходимо ввести число с плавающей точкой.');
    Exit;
  end;

  if plan1 < 0 Then Begin
    ShowMessage('План зенитного угла быть больше либо равен 0.');
    Exit;
  End;

  Try
    plan2 := StrToInt(Trim(e4.Text));
  Except
    ShowMessage('Ошибка ввода плана азимута. Необходимо ввести целое число.');
    Exit;
  end;

  // Ввели interval, plan1, plan2
  // Поиск в файле: finterval, fakt1, fakt2

  AssignFile(f, 'xx.txt');
  ReSet(f);

  // Чтение строки заголовка.
  Readln(f, str);

  // Флаг - не нашли.
  found := false;

  // Чтение строк записей.
  While not Eof(f) do Begin

    // Чтение всей строки с числами.
    Readln(f, str);

    // Если пустая строка (может быть в конце файла)
    if Length(str) < 5 Then
      break;

    // Разбиение строки по числам-строкам.
    numbers := Split(str);

    // Переводим числа-строки в числа.
    finterval := StrToInt(numbers[1]);
    fakt1 := StrToFloat(numbers[2]);
    fakt2 := StrToInt(numbers[3]);

    if finterval = interval Then Begin
      itog1 := (fakt1 - plan1) / plan1 * 100;
      itog2 := (fakt2 - plan2) / plan2 * 100;
      e2.Text := FloatToStr(RoundTo(fakt1, -1));
      e5.Text := IntToStr(fakt2);
      e3.Text := FloatToStr(RoundTo(itog1, -1));
      e6.Text := FloatToStr(RoundTo(itog2, -1));
      found := true;
      break;
    End;
  End;
  CloseFile(f);

  // Если не нашли стираем.
  if not found Then Begin
    e2.Clear;
    e3.Clear;
    e5.Clear;
    e6.Clear;
    ShowMessage('Интервал не найден.');
  End;
end;

end.
