+++
title = "Magic squares/Perl"
description = ""
date = 2019-05-04T23:38:10Z
aliases = []
[extra]
id = 22308
[taxonomies]
categories = []
tags = []
+++

Rather than having multiple examples for different orders of magic square, this program generates a magic square for ''any'' valid n x n grid.

This page is referenced from:<ul>
<li>[[Magic_squares_of_odd_order#Perl|Magic squares of odd order#Perl]]</li>
<li>[[Magic_squares_of_singly_even_order#Perl|Magic squares of singly even order#Perl]]</li>
<li>[[Magic_squares_of_doubly_even_order#Perl|Magic squares of doubly even order#Perl]]</li>
</ul>


## Perl

{{trans|Perl 6}}

```perl
use strict;
use warnings;
use List::Util 'sum';

my(@sq,$i,$h,$q);

for my $n (3..12,31) {
    $i = 1;
    $h = int($n / 2);
    $q = int($n / 4);
    generate_magic($n);
    validate_magic();
    printf("N = $n, magic number = %d\n", sum @{$sq[0]});
    printf(("%@{[1+length($n**2)]}d"x$n)."\n",@$_) for @sq;
    print "\n";
}

sub generate_magic {
    my($n) = @_;

    if ($n <= 2) {
        print "Sorry, can not generate a $n x $n magic square.\n" and return;

    } elsif ($n % 2) { # odd
        my $x = $n/2;
        my $y = 0;
        for (0 .. $n**2-1) {
            $sq[($i%$n ? $y-- : $y++) % $n][($i%$n ? $x++ : $x) % $n] = $i;
            $i++;
        }

    } elsif (0 == int $n%4) { # doubly even
        my $x = 0;
        my $y = 0;
        for (0 .. $n**2-1) {
            $sq[$i % $n ? $y : $y++][($i-1) % $n] = $i;
            $i++;
        }
        for my $r (0..$q-1) {
            for my $c ($q .. $n-$q-1) {
                swap( ($r,$c), ($n-1-$r,$n-1-$c) );
                swap( ($c,$r), ($n-1-$c,$n-1-$r) );
            }
        }

    } elsif (0 == int($n%2) && $n%4) { # singly even
        generate_magic($h);
        $i *= 4;
        for my $r (0..$h-1) {
            for my $c (0..$h-1) {
                $sq[$r+$h][$c   ] = $sq[$r][$c] + $h**2 * 3;
                $sq[$r   ][$c+$h] = $sq[$r][$c] + $h**2 * 2;
                $sq[$r+$h][$c+$h] = $sq[$r][$c] + $h**2;
            }
            for my $c (0..$q-1) {
                next if $c == 0 and $r == int(($h-1)/2);
                swap( ($r,$c), ($r+$h,$c) );
            }
            if ($h > 4) {
                swap( ($r,$_), ($r+$h,$_) ) for $n-$q+1 .. $n-1;
            }
        }
        swap( ($q,$q), ($q+$h,$q) );
    }
}

sub swap {
    my($a,$b,$c,$d) = @_;
    ($sq[$a][$b], $sq[$c][$d]) = ($sq[$c][$d], $sq[$a][$b]);
}

sub validate_magic {
    my $magic = sum @{$sq[0]};
    my @transpose;
    foreach my $j (0..$#{$sq[0]}) {
        push(@transpose, [map $_->[$j], @sq]);
    }
    for (0..$#sq) {
        die unless $magic == sum @{ $sq[$_]} and $magic == sum @{$transpose[$_]}
    }
}
```

{{out}}

```txt
N = 3, magic number = 15
 8 1 6
 3 5 7
 4 9 2

N = 4, magic number = 34
  1 15 14  4
 12  6  7  9
  8 10 11  5
 13  3  2 16

N = 5, magic number = 65
 17 24  1  8 15
 23  5  7 14 16
  4  6 13 20 22
 10 12 19 21  3
 11 18 25  2  9

N = 6, magic number = 111
 35  1  6 26 19 24
  3 32  7 21 23 25
 31  9  2 22 27 20
  8 28 33 17 10 15
 30  5 34 12 14 16
  4 36 29 13 18 11

N = 7, magic number = 175
 30 39 48  1 10 19 28
 38 47  7  9 18 27 29
 46  6  8 17 26 35 37
  5 14 16 25 34 36 45
 13 15 24 33 42 44  4
 21 23 32 41 43  3 12
 22 31 40 49  2 11 20

N = 8, magic number = 260
  1  2 62 61 60 59  7  8
  9 10 54 53 52 51 15 16
 48 47 19 20 21 22 42 41
 40 39 27 28 29 30 34 33
 32 31 35 36 37 38 26 25
 24 23 43 44 45 46 18 17
 49 50 14 13 12 11 55 56
 57 58  6  5  4  3 63 64

N = 9, magic number = 369
 47 58 69 80  1 12 23 34 45
 57 68 79  9 11 22 33 44 46
 67 78  8 10 21 32 43 54 56
 77  7 18 20 31 42 53 55 66
  6 17 19 30 41 52 63 65 76
 16 27 29 40 51 62 64 75  5
 26 28 39 50 61 72 74  4 15
 36 38 49 60 71 73  3 14 25
 37 48 59 70 81  2 13 24 35

N = 10, magic number = 505
  92  99   1   8  15  67  74  51  58  40
  98  80   7  14  16  73  55  57  64  41
   4  81  88  20  22  54  56  63  70  47
  85  87  19  21   3  60  62  69  71  28
  86  93  25   2   9  61  68  75  52  34
  17  24  76  83  90  42  49  26  33  65
  23   5  82  89  91  48  30  32  39  66
  79   6  13  95  97  29  31  38  45  72
  10  12  94  96  78  35  37  44  46  53
  11  18 100  77  84  36  43  50  27  59

N = 11, magic number = 671
  68  81  94 107 120   1  14  27  40  53  66
  80  93 106 119  11  13  26  39  52  65  67
  92 105 118  10  12  25  38  51  64  77  79
 104 117   9  22  24  37  50  63  76  78  91
 116   8  21  23  36  49  62  75  88  90 103
   7  20  33  35  48  61  74  87  89 102 115
  19  32  34  47  60  73  86  99 101 114   6
  31  44  46  59  72  85  98 100 113   5  18
  43  45  58  71  84  97 110 112   4  17  30
  55  57  70  83  96 109 111   3  16  29  42
  56  69  82  95 108 121   2  15  28  41  54

N = 12, magic number = 870
   1   2   3 141 140 139 138 137 136  10  11  12
  13  14  15 129 128 127 126 125 124  22  23  24
  25  26  27 117 116 115 114 113 112  34  35  36
 108 107 106  40  41  42  43  44  45  99  98  97
  96  95  94  52  53  54  55  56  57  87  86  85
  84  83  82  64  65  66  67  68  69  75  74  73
  72  71  70  76  77  78  79  80  81  63  62  61
  60  59  58  88  89  90  91  92  93  51  50  49
  48  47  46 100 101 102 103 104 105  39  38  37
 109 110 111  33  32  31  30  29  28 118 119 120
 121 122 123  21  20  19  18  17  16 130 131 132
 133 134 135   9   8   7   6   5   4 142 143 144

N = 31, magic number = 14911
 498 531 564 597 630 663 696 729 762 795 828 861 894 927 960   1  34  67 100 133 166 199 232 265 298 331 364 397 430 463 496
 530 563 596 629 662 695 728 761 794 827 860 893 926 959  31  33  66  99 132 165 198 231 264 297 330 363 396 429 462 495 497
 562 595 628 661 694 727 760 793 826 859 892 925 958  30  32  65  98 131 164 197 230 263 296 329 362 395 428 461 494 527 529
 594 627 660 693 726 759 792 825 858 891 924 957  29  62  64  97 130 163 196 229 262 295 328 361 394 427 460 493 526 528 561
 626 659 692 725 758 791 824 857 890 923 956  28  61  63  96 129 162 195 228 261 294 327 360 393 426 459 492 525 558 560 593
 658 691 724 757 790 823 856 889 922 955  27  60  93  95 128 161 194 227 260 293 326 359 392 425 458 491 524 557 559 592 625
 690 723 756 789 822 855 888 921 954  26  59  92  94 127 160 193 226 259 292 325 358 391 424 457 490 523 556 589 591 624 657
 722 755 788 821 854 887 920 953  25  58  91 124 126 159 192 225 258 291 324 357 390 423 456 489 522 555 588 590 623 656 689
 754 787 820 853 886 919 952  24  57  90 123 125 158 191 224 257 290 323 356 389 422 455 488 521 554 587 620 622 655 688 721
 786 819 852 885 918 951  23  56  89 122 155 157 190 223 256 289 322 355 388 421 454 487 520 553 586 619 621 654 687 720 753
 818 851 884 917 950  22  55  88 121 154 156 189 222 255 288 321 354 387 420 453 486 519 552 585 618 651 653 686 719 752 785
 850 883 916 949  21  54  87 120 153 186 188 221 254 287 320 353 386 419 452 485 518 551 584 617 650 652 685 718 751 784 817
 882 915 948  20  53  86 119 152 185 187 220 253 286 319 352 385 418 451 484 517 550 583 616 649 682 684 717 750 783 816 849
 914 947  19  52  85 118 151 184 217 219 252 285 318 351 384 417 450 483 516 549 582 615 648 681 683 716 749 782 815 848 881
 946  18  51  84 117 150 183 216 218 251 284 317 350 383 416 449 482 515 548 581 614 647 680 713 715 748 781 814 847 880 913
  17  50  83 116 149 182 215 248 250 283 316 349 382 415 448 481 514 547 580 613 646 679 712 714 747 780 813 846 879 912 945
  49  82 115 148 181 214 247 249 282 315 348 381 414 447 480 513 546 579 612 645 678 711 744 746 779 812 845 878 911 944  16
  81 114 147 180 213 246 279 281 314 347 380 413 446 479 512 545 578 611 644 677 710 743 745 778 811 844 877 910 943  15  48
 113 146 179 212 245 278 280 313 346 379 412 445 478 511 544 577 610 643 676 709 742 775 777 810 843 876 909 942  14  47  80
 145 178 211 244 277 310 312 345 378 411 444 477 510 543 576 609 642 675 708 741 774 776 809 842 875 908 941  13  46  79 112
 177 210 243 276 309 311 344 377 410 443 476 509 542 575 608 641 674 707 740 773 806 808 841 874 907 940  12  45  78 111 144
 209 242 275 308 341 343 376 409 442 475 508 541 574 607 640 673 706 739 772 805 807 840 873 906 939  11  44  77 110 143 176
 241 274 307 340 342 375 408 441 474 507 540 573 606 639 672 705 738 771 804 837 839 872 905 938  10  43  76 109 142 175 208
 273 306 339 372 374 407 440 473 506 539 572 605 638 671 704 737 770 803 836 838 871 904 937   9  42  75 108 141 174 207 240
 305 338 371 373 406 439 472 505 538 571 604 637 670 703 736 769 802 835 868 870 903 936   8  41  74 107 140 173 206 239 272
 337 370 403 405 438 471 504 537 570 603 636 669 702 735 768 801 834 867 869 902 935   7  40  73 106 139 172 205 238 271 304
 369 402 404 437 470 503 536 569 602 635 668 701 734 767 800 833 866 899 901 934   6  39  72 105 138 171 204 237 270 303 336
 401 434 436 469 502 535 568 601 634 667 700 733 766 799 832 865 898 900 933   5  38  71 104 137 170 203 236 269 302 335 368
 433 435 468 501 534 567 600 633 666 699 732 765 798 831 864 897 930 932   4  37  70 103 136 169 202 235 268 301 334 367 400
 465 467 500 533 566 599 632 665 698 731 764 797 830 863 896 929 931   3  36  69 102 135 168 201 234 267 300 333 366 399 432
 466 499 532 565 598 631 664 697 730 763 796 829 862 895 928 961   2  35  68 101 134 167 200 233 266 299 332 365 398 431 464