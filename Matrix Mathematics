local module = {}
local rng = Random.new(tick())

local function MatrixDetection(Matrix, errmsg) --matrix error detection
	if type(Matrix) ~= "table" then 
		error(errmsg)
	elseif #Matrix == 0 then
		error(errmsg)
	else
		for i = 1,#Matrix do
			if type(Matrix[i]) ~= "table" then
				error(errmsg)
			elseif #Matrix[i] == 0 then
				error(errmsg)
			else
				for o = 1,#Matrix[i] do
					if type(Matrix[i][o]) ~= "number" then
						error(errmsg)
					end
				end
			end
		end
	end
end



function module.CreateRandom(Size, MinNumSize, MaxNumSize)
	
	--error detection
	if type(MinNumSize) ~= "number" then
		error("MinNumSize must be a number.(Arg2)")
	elseif type(MaxNumSize) ~= "number" then
		error("MinNumSize must be a number.(Arg2)")
	elseif type(Size) ~= "table" then
		error("Matrix size must be a table.(Arg1)")
	elseif MinNumSize >= MaxNumSize then
		error("Minimum must be less than Maximum.(Arg3)")
	elseif Size[1]<1 or Size[2]<1 then
		error("Size of Matrix must be at least 1x1.(Arg1)")
	end
	
	
	--setting up matrix value sizes
	local Min = 0
	if MinNumSize >= 0 then
		Min = MinNumSize*1000000
	else
		Min = (MinNumSize+1)*1000000
	end
	
	local Max = 0
	if MaxNumSize >= 0 then
		Max = (MaxNumSize-1)*1000000
	else
		Max = MaxNumSize*1000000
	end
	
	
	--creating matrix
	local Matrix = {}
	for i = 1,Size[2] do
		local row = {}
		for o = 1,Size[1] do
			row[o] = rng:NextNumber(Min, Max)/1000000
		end
		Matrix[i] = row
	end
	
	return Matrix
end

function module.Transpose(Matrix)
	
	--error detection
	MatrixDetection(Matrix, "Argument must be a valid Matrix.(Arg1)")
	
	--create new matrix
	local NewMatrix = {}
	for i = 1,#Matrix[1] do
		NewMatrix[i] = {}
	end
	
	--transpose matrix
	local rownum = #Matrix[1]
	for i = 1,#Matrix do
		for o = 1,rownum do
			NewMatrix[o][i] = Matrix[i][o]
		end
	end
	
	return NewMatrix
end


function module.ScalarMultiply(Scalar, Matrix)
	
	--error detection
	if type(Scalar) ~= "number" then
		error("Scalar must be a number.(Arg1)")
	else
		MatrixDetection(Matrix, "Arg2 must be a valid Matrix.(Arg2)")
	end
	
	--scalar multiplying
	local NewMatrix = Matrix
	local rownum = #Matrix[1]
	for i = 1,#NewMatrix do
		for o = 1,rownum do
			NewMatrix[i][o] = NewMatrix[i][o]*Scalar
		end
	end
	
	return NewMatrix
end

function module.Add(MatrixA, MatrixB)
	
	--error detection
	MatrixDetection(MatrixA, "Matrix A is not a valid Matrix.(Arg1)")
	MatrixDetection(MatrixB, "Matrix B is not a valid Matrix.(Arg2)")
	local err = {}
	if #MatrixA ~= #MatrixB or #MatrixA[1] ~= #MatrixB[1] then
		error("matrices must be the same size.(Arg1/Arg2)")
	end
	
	--add the matrices together
	local rownum = #MatrixA[1]
	local NewMatrix = MatrixA --MatrixA is not used in this context, its simply to get the size of the matrix.
	for i = 1,#MatrixA do
		for o = 1,rownum do
			NewMatrix[i][o] = MatrixA[i][o]+MatrixB[i][o]
		end
	end
	
	return NewMatrix
end

function module.Multiply(MatrixA, MatrixB)
	
	--error detetion
	MatrixDetection(MatrixA, "Matrix A is not a valid Matrix.(Arg1)")
	MatrixDetection(MatrixB, "Matrix B is not a valid Matrix.(Arg2)")
	if #MatrixA[1] ~= #MatrixB then
		error("The number of rows in MatrixA and columns in MatrixB must be equal.(Arg1/Arg2)")
	end
	
	local colnum = #MatrixA
	local midnum = #MatrixB
	local rownum = #MatrixB[1]
	
	--create the new matrix
	local NewMatrix = {}
	for i = 1,colnum do
		NewMatrix[i] = {}
		for o = 1,rownum do
			NewMatrix[i][o] = 0
		end
	end
	
	--matrix multiplication
	for i = 1,colnum do
		for o = 1,rownum do
			for p = 1,midnum do
				NewMatrix[i][o] = NewMatrix[i][o]+MatrixA[i][p]*MatrixB[p][o]
			end
		end
	end
	
	return NewMatrix
end

return module
