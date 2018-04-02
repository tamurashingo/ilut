##############################################################################
# Sample Makefile.
#
#   Copyright (c) 2008 tamura shingo
##############################################################################

##############################################################################
# Makefile定義
#
######################################
# ユニットテストの実行
######################################
ut : .unittest

######################################
# 再構築
######################################
rebuild : .clean .unittest

######################################
# クリーンアップ
######################################
clean : .clean


##############################################################################
# コンパイルルールの定義
##############################################################################
CC=			gcc
AR=			ar
LINK=		gcc
FLEX=		flex
AWK=		awk

CFLAGS=		-g -Wall
INCLUDES=	-I$(SRCDIR)
LDFLAGS=	-L. -ll
ARFLAGS=	rcsv
LFLAGS=

SRCDIR=		./
TESTDIR=	../

.c.o :
	$(CC) -c $(CFLAGS) $(INCLUDES) -o $@ $<

##############################################################################
# ビルド
##############################################################################
$(SRCDIR)/options.o: $(SRCDIR)/options.h

##############################################################################
# アプリケーションのクリーンアップ
##############################################################################
.clean :
	rm -rf *~ $(SRCDIR)/*.o $(SRCDIR)/*~


##############################################################################
# ユニットテストのルール定義
##############################################################################
INCLUDES=		-I$(SRCDIR) -I$(TESTDIR)
SAMPLEDIR=		$(TESTDIR)/sample

TOOLDIR=		../tool

.unittest : ut_clean ut_tool ut_options
	$(AWK) -f $(TOOLDIR)/ilut2xml.awk $(SAMPLEDIR)/options.result > ilut_result.xml
	@echo "All tests successful."


######################################
# ユニットテストのクリーンアップ
######################################
ut_clean :
	rm -f $(TESTDIR)/ILUT.o
	rm -f $(SAMPLEDIR)/test_options.o
	rm -f $(SAMPLEDIR)/options.o
	rm -f $(SAMPLEDIR)/test_options
	rm -f $(SAMPLEDIR)/options.result
	rm -f ilut_result.xml


######################################
# ユニットテストツールのコンパイル
######################################
ut_tool : $(TESTDIR)/ILUT.o

$(TESTDIR)/ILUT.o : $(TESTDIR)/ILUT.h


######################################
# ユニットテスト
######################################
ut_options : $(SAMPLEDIR)/test_options.o $(SAMPLEDIR)/options.o
	$(LINK) -o $(SAMPLEDIR)/test_options $(SAMPLEDIR)/test_options.o $(SAMPLEDIR)/options.o $(TESTDIR)/ILUT.o $(LDFLAGS)
	$(SAMPLEDIR)/test_options $(SAMPLEDIR)/options.result

$(SAMPLEDIR)/test_options.o : $(SRCDIR)/options.h


