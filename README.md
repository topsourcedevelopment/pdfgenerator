About
============

This is the latest mpdf 6 compatibility with PHP7.4

fixed the below four warnings which appeared in the mpdf class file:

Warning1: PHP Warning:  A non-numeric value encountered in mpdf60\mpdf.php on line 17033 
Action1:  Original line of code was:

if (($setwidth + $currblk['margin_left'] + $currblk['margin_right'] + $bdl + $pdl + $bdr + $pdr) > $maxw || ($maxw - ($currblk['margin_right'] + $currblk['margin_left'] + $bdl + $pdl + $bdr + $pdr)) < (2*$this->GetCharWidth('W',false))) {

added a function “get_numeric” at the end in class file and changed the code to:

if (($this->get_numeric($setwidth) + $this->get_numeric($currblk['margin_left']) + $this->get_numeric($currblk['margin_right']) + $this->get_numeric($bdl) + $this->get_numeric($pdl) + $this->get_numeric($bdr) + $this->get_numeric($pdr)) > $this->get_numeric($maxw) || ($this->get_numeric($maxw) - ($this->get_numeric($currblk['margin_right']) + $this->get_numeric($currblk['margin_left']) + $this->get_numeric($bdl) + $this->get_numeric($pdl) + $this->get_numeric($bdr) + $this->get_numeric($pdr))) < (2*$this->get_numeric($this->GetCharWidth('W',false)))) {


Warning2: PHP Warning:  A non-numeric value encountered in mpdf60\mpdf.php on line 17150
Action2:  Original line of code was:

$currblk['inner_width'] = $currblk['width'] - ($currblk['border_left']['w'] + $currblk['padding_left'] + $currblk['border_right']['w'] + $currblk['padding_right']);

used the same function “get_numeric” and changed the code to:

$currblk['inner_width'] = $this->get_numeric($currblk['width']) - ($this->get_numeric($currblk['border_left']['w']) + $this->get_numeric($currblk['padding_left']) + $this->get_numeric($currblk['border_right']['w']) + $this->get_numeric($currblk['padding_right']));


Warning3: PHP Warning:  A non-numeric value encountered in mpdf60\mpdf.php on line 5559
Action3:  Original line of code was:

$paddingR = ($ipaddingR * _MPDFK);

Used the same function “get_numeric” and changed the code to:

$paddingR = ($this->get_numeric($ipaddingR) * _MPDFK);


Warning4: PHP Warning:  A non-numeric value encountered in mpdf60\mpdf.php on line 17147
Action4:  Original line of code was:

$currblk['outer_right_margin'] = $prevblk['outer_right_margin']  + $currblk['margin_right'] + $prevblk['border_right']['w'] + $prevblk['padding_right']; 

used the same function “get_numeric” and changed the code to:

$currblk['outer_right_margin'] = $this->get_numeric($prevblk['outer_right_margin'])  + $this->get_numeric($currblk['margin_right']) + $this->get_numeric($prevblk['border_right']['w']) + $this->get_numeric($prevblk['padding_right']);


Function get_numeric is defined as below:
function get_numeric($val) 
{
  if (is_numeric($val)) {
    return $val + 0;
  }
  return 0;
}

